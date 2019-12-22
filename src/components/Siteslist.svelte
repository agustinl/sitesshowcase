<script>
    import { Link } from "svelte-routing";
    import Icon from 'fa-svelte';
    import { faTwitter } from '@fortawesome/free-brands-svg-icons/faTwitter';
    import { faGithub } from '@fortawesome/free-brands-svg-icons/faGithub';
    import { faDribbble } from '@fortawesome/free-brands-svg-icons/faDribbble';
    import { faLinkedin } from '@fortawesome/free-brands-svg-icons/faLinkedin';
    import { faBehance } from '@fortawesome/free-brands-svg-icons/faBehance';

    let twitter = faTwitter;
    let github = faGithub;
    let dribbble = faDribbble;
    let linkedin = faLinkedin;
    let behance = faBehance;
    let reportID;

	export let sites;
    export let pages;
    export let page;
    export let error;
    
</script>

<style>
h3 {
    color: #000;
    text-align:center;
}

.no-site {
    width: 100%;
    margin-bottom: 30px;
}

article p:nth-child(3) {
    margin-bottom:5px;
}

article p:last-child {
    visibility:hidden;
    text-align:right;
    text-transform:uppercase;
    margin-bottom:5px;
}

article p:last-child a {
    color:#737373;
}

article:hover p:last-child {
    visibility:visible;
}
</style>

<div class="container" id="sites-list">

    {#if sites}
        {#each sites as site, i}
            <article id={i}>
                <a href="{site.websiteurl}?ref=sitesshowcase" aria-label={site.website} rel="noopener noreferrer" target="_blank"><img src={site.image} alt={site.website}></a>
                <div class="info">
                    <h5><a href="{site.websiteurl}?ref=sitesshowcase" rel="noopener noreferrer" target="_blank">{site.website}</a></h5>
                    {#if site.author[0].social == "twitter"}
                        <p>by <a href="https://twitter.com/{site.author[0].author}?ref=sitesshowcase" rel="noopener noreferrer" target="_blank">@{@html site.author[0].author} <Icon icon={twitter}></Icon></a></p>
                    {:else if site.author[0].social == "github"}
                        <p>by <a href="https://github.com/{site.author[0].author}?ref=sitesshowcase" rel="noopener noreferrer" target="_blank">@{@html site.author[0].author} <Icon icon={github}></Icon></a></p>
                    {:else if site.author[0].social == "linkedin"}
                        <p>by <a href="https://www.linkedin.com/in/{site.author[0].author}?ref=sitesshowcase" rel="noopener noreferrer" target="_blank">@{@html site.author[0].author} <Icon icon={linkedin}></Icon></a></p>
                    {:else if site.author[0].social == "dribbble"}
                        <p>by <a href="https://dribbble.com/{site.author[0].author}?ref=sitesshowcase" rel="noopener noreferrer" target="_blank">@{@html site.author[0].author} <Icon icon={dribbble}></Icon></a></p>
                    {:else if site.author[0].social == "behance"}
                        <p>by <a href="https://www.behance.net/{site.author[0].author}?ref=sitesshowcase" rel="noopener noreferrer" target="_blank">@{@html site.author[0].author} <Icon icon={behance}></Icon></a></p>
                    {/if}
                    <p>{@html site.description}</p>
                    <p><small><Link to="contact?id={site._id}">Report</Link></small></p>
                </div>
            </article>
        {:else}
			<div class="no-site">
                <h3>There is no website uploaded yet, be the first!</h3>
            </div>
		{/each}
    {:else if error}
		<div class="no-site">
            <h3>{error}</h3>
        </div>
    {:else}
        <div id="loading">
            <div class="spinner"></div>
        </div>
    {/if}

</div>

<div class="container" id="pagination">
    {#if page < pages && page == 1}
        <div></div>
        <a href="/#/page/{ page + 1 }" rel="prefetch" class="button button-primary">Next</a>
    {:else if page < pages && page > 1}        
        <a href="/#/page/{ page - 1 }" class="button button-primary">Previous</a>          
        <a href="/#/page/{ page + 1 }" rel="prefetch" class="button button-primary">Next</a>
    {:else if page >= pages && page != 1}        
        <a href="/#/page/{ page - 1 }" class="button button-primary">Previous</a>
        <div></div>
    {/if}
</div>