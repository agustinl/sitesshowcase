<script>
    import { Link } from "svelte-routing";
    import Icon from 'fa-svelte';    
    import { fade } from 'svelte/transition';
    import { faGithub } from '@fortawesome/free-brands-svg-icons/faGithub';

    let github = faGithub;
</script>

<style>
footer {
    border-top: solid 1px #ececec;
    margin-top: 20px;
    padding: 20px 0;
}

.footer-buttons {
    display:flex;
    align-items:center;

    margin-bottom: 20px;
}
</style>

<footer class="container" transition:fade>

    <div class="footer-buttons">        
        <style>.bmc-button img{width: 35px !important;margin-bottom: 1px !important;box-shadow: none !important;border: none !important;vertical-align: middle !important;}.bmc-button{padding: 7px 10px 7px 10px !important;line-height: 35px !important;height:51px !important;min-width:217px !important;text-decoration: none !important;display:inline-flex !important;color:#FFFFFF !important;background-color:#FF813F !important;border-radius: 5px !important;border: 1px solid transparent !important;padding: 7px 10px 7px 10px !important;font-size: 22px !important;letter-spacing: 0.6px !important;box-shadow: 0px 1px 2px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;margin: 0 auto !important;font-family:'Cookie', cursive !important;-webkit-box-sizing: border-box !important;box-sizing: border-box !important;-o-transition: 0.3s all linear !important;-webkit-transition: 0.3s all linear !important;-moz-transition: 0.3s all linear !important;-ms-transition: 0.3s all linear !important;transition: 0.3s all linear !important;}.bmc-button:hover, .bmc-button:active, .bmc-button:focus {-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;text-decoration: none !important;box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;opacity: 0.85 !important;color:#FFFFFF !important;}</style><link href="https://fonts.googleapis.com/css?family=Cookie" rel="stylesheet"><a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/agustinl" rel="noopener noreferrer"><img src="https://cdn.buymeacoffee.com/buttons/bmc-new-btn-logo.svg" alt="Buy me a beer"><span style="margin-left:15px;font-size:28px !important;">Buy me a beer</span></a>
    </div>

    <h6>Any problems or suggestions? <Link to="/contact">Contact</Link></h6>
    <h6>Made with <a href="https://svelte.dev/" rel="noopener noreferrer" target="_blank">sveltejs</a> deployed with <a href="https://zeit.co/home" rel="noopener noreferrer" target="_blank">▲ ZEIT Now</a> </h6>
    <h6>{new Date().getFullYear()} - Made with 🧉 in Argentina</h6>
    <h6><a href="https://github.com/agustinl/sitesshowcase" aria-label="GitHub Repo"><Icon icon={github}></Icon></a></h6>

</footer>