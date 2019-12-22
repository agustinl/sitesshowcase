<script>
	import { onMount } from 'svelte';
	import Hero from '../components/Hero.svelte';
    import Footer from '../components/Footer.svelte';
    
    let reportid = 0;

    let contactmessage;
    
    $: message = "";

    onMount(async () => {
        var url = new URL(window.location.href);
        var search_params = new URLSearchParams(url.search); 
        
        if(search_params.has('id')) {
            reportid = search_params.get('id');
        }
	});

    async function handleSubmit() {
        
        var data = {contactmessage: contactmessage};

        const response = await fetch(`API_URL/contact?id=${reportid}`, {
        method: 'POST',
        body: JSON.stringify(data),
        headers:{
            'Content-Type': 'application/json'
        }
        })   

        var responseMessage = await response.json();

        if (response.ok) {
            document.getElementById("contact-form").reset();
            contactmessage = "";
            message = responseMessage.msg;
        } else {
            if(response.status === 429) {
                message = responseMessage.msg;
            } else if(response.status === 422) {
                message = responseMessage.msg[0].msg;
            } else {
                message = responseMessage.msg;
            }
            throw Error(response.statusText);
        }

    }

    function resetform() {
		document.getElementById("contact-form").reset();
        contactmessage = "";
    }
</script>

<style>
.form-buttons {
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-pack:end;
        -ms-flex-pack:end;
            justify-content:flex-end;
}

.form-buttons button:first-child {
    margin-right: 20px;
}

.msg-info h4 {
    color: #000;
    text-align:left;
}

::-webkit-input-placeholder {
    color: #888;
    font-size: 14px;
}

:-ms-input-placeholder {
    color: #888;
    font-size: 14px;
}

::-moz-placeholder {
    color: #888;
    font-size: 14px;
}

::-ms-input-placeholder {
    color: #888;
    font-size: 14px;
}

::placeholder {
    color: #888;
    font-size: 14px;
}
</style>

<svelte:head>
	<title>Contact | Sites showcase</title>
</svelte:head>

<Hero />

<div id="contact" class="container">

    <form id="contact-form" on:submit|preventDefault={handleSubmit}>
        <textarea type="text" placeholder="Where can you tell us what you want..." bind:value={ contactmessage }></textarea>
        <div class="form-buttons">
            <a href="." type="reset" class="button-secondary" on:click={resetform}>Cancel</a>
            <button type="submit" class="button-primary" disabled={!contactmessage}>Send</button>
        </div>
    </form>

    <div class="msg-info">
    {#if message}
        <h4>{message}</h4>
    {/if}
    </div>

</div>

<Footer />