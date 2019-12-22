<script>
	import { onMount } from 'svelte';
    import { Link } from "svelte-routing";
    import { fade } from 'svelte/transition';
    import fetch from 'node-fetch';

    let visible = true;
    let websiteok = false;
    let website;
    let author;
    let social;
    let total;        
    let regex = RegExp('[ |,|\?|\*|\+|\#|\&|\%|\$|\^]');

    $: message = "";

    async function totalSites() {
        await fetch(`API_URL/all`)
        .then(r => r.json())
        .then(data => {
            total = data.total;
        });
    }
    
    async function handleSubmit() {
        
        message = "Submitting your site...";
        var data = {website: website, author: author, social: social};

        if(regex.test(website)) {
            websiteok = false;
            message = "We need a site like this: http://www.mysite.com"; 
        } else {
            const response = await fetch(`API_URL`, {
            method: 'POST',
            body: JSON.stringify(data),
            headers:{
                'Content-Type': 'application/json'
            }
            })
            
            var responseMessage = await response.json();

            if (response.ok) {
                message = responseMessage.msg;
                setTimeout(function(){
                    location.reload();
                }, 2000);
            } else {
                if(response.status === 418) {
                    message = responseMessage.msg;
                } else if (response.status === 429) {
                    message = responseMessage.msg;
                } else {
                    message = responseMessage.msg;
                }
                throw Error(response.statusText);
            }
        }

    }

    function websiteRegex(event) {

        if (website && !website.match(/^http([s]?):\/\/.*/)) {
            website = 'http://' + website;
        }

        if(regex.test(website)) {
            websiteok = false;
            message = "We need a site like this: http://www.mysite.com";
        } else {
            websiteok = true;
            message = "";
        }

    }

    function resetform() {
        visible = true;
		document.getElementById("upload-form").reset();
		website = "";
		author = "";
		message = "";
    }
    
    onMount(totalSites);

</script>

<style>
</style>

<header class="container">
	<nav>
		<ul>
			<li>
                <h1 class="logo">                
                    <Link to="/" title="sitesshowcase" >
                        <img src="logo.svg" alt="sitesshowcase">
                    </Link>
                </h1>
            </li>
			<li>
				<button class="button button-primary" on:click="{() => visible = false}">Submit My Site</button>
			</li>
		</ul>
	</nav>
</header>

<section class="container-fluid heros">

    {#if visible}
    <section id="home-hero" class="hero" transition:fade>

        <div class="hh-left">
            <h2>Inspiration for</h2>
            <div class="slidingVertical">
                <span>{'<developers/>'}</span>
                <span>DeSiGnErS.·*</span>
                <span>curio.Ous</span>
            </div>
        </div>

        <div class="hh-right">
            <div>
                <h3>A community list <br> of personal sites <br> for inspiration</h3>
                <hr>
            </div>
            <div>
                {#if total && total > 0}
                    <h4>{total} uploaded sites</h4>
                {/if}
            </div>
        </div>

    </section>

    {:else}

    <section id="form-hero" class="hero" transition:fade>

        <div class="fh-left">
            <h2>Submit my site</h2>
        </div>

        <div class="fh-right">
            <div>
                <form id="upload-form" on:submit|preventDefault={handleSubmit}>
                    <input type="text" placeholder="http://www.mysite.com" bind:value={ website } on:change={websiteRegex} maxlength="80">
                    <div class="form-group">
                        <select name="social" id="social" bind:value={social}>
                            <option value="twitter">twitter</option>
                            <option value="github">github</option>
                            <option value="linkedin">linkedin</option>
                            <option value="dribbble">dribbble</option>
                            <option value="behance">behance</option>
                        </select>
                        <input type="text" placeholder="author" bind:value={ author } maxlength="80">                        
                    </div>
                    <div class="form-buttons">
                        <button type="reset" class="button-neutral" on:click={resetform}>Cancel</button>
                        <button type="submit" class="button-secondary" disabled={!websiteok || !author}>Submit</button>
                    </div>
                </form>
                <hr>
            </div>
            <div>
                {#if message}
                    <h4>{message}</h4>
                {/if}
            </div>
        </div>

    </section>
    {/if}

</section>