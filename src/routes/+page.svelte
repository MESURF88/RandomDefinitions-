<script lang="ts">
    type ReturnedDefinition = {
        word: string
        definition: string
        example: string
	}

    let invalidResponse = $state<boolean>(false)
    let termValueName = $state<string>("")
    let returnedDef = $state<ReturnedDefinition>({ word: "", definition: "", example: ""})

    function resetForm()
    {
        termValueName = ""
        invalidResponse = false
    }

	function getData() {
        getDataTerm(termValueName)
	}

    async function getDataTerm(term: string) {
        const url = term === ""? 'https://api.urbandictionary.com/v0/random' : "https://api.urbandictionary.com/v0/define?term=" + term;
        const response = await fetch(
            url,
            {
                method: 'GET'
            }
        );
        if (response.status == 200)
        {
            const data = await response.json();
            // get the one with most thumbs up from list
            if (data.list.length > 0)
            {
                const sortedlist = data.list.sort(function(a: any, b: any) { 
                    return Number(b.thumbs_up) - Number(a.thumbs_up);
                })
                const hv = sortedlist[0];
                // .word .definition .example
                returnedDef = {word: hv.word, definition: hv.definition, example: hv.example }
                invalidResponse = false
            }
            else 
            {
                invalidResponse = true
            }
        }
        else
        {
            invalidResponse = true
            console.error("Failed GET of term");
        }
    }

  
    function currentWord() {
		return returnedDef.word
	}

    function currentDefinition() {
		return returnedDef.definition.replaceAll( "[","" ).replaceAll( "]","" ) 
	}

    function currentExample() {
		return returnedDef.example.replaceAll( "[","" ).replaceAll( "]","" ) 
	}
</script>


<div id="top" class="jw-is-slideshow jw-header-is-text jw-is-segment-page jw-is-frontend jw-is-no-sidebar jw-is-no-messagebar jw-is-no-touch-device jw-is-no-mobile jw-menu-is-desktop jw-is-header-affix" data-jouwweb-page="25571451" data-jouwweb-segment-id="25571451" data-jouwweb-segment-type="page" data-template-threshold="800" data-template-name="modern|skyline"  itemtype="https://schema.org/WebSite">
    <meta itemprop="url" content="https://temp-emuqgvvvthytptgpyjki.webadorsite.com/">
<div class="jw-background"></div>
<div class="jw-body">
<div class="jw-mobile-menu jw-mobile-is-text js-mobile-menu">
<span class="jw-mobile-menu__button jw-mobile-menu__button--dummy"></span>        <div class="jw-mobile-header jw-mobile-header--text">
<span class="jw-mobile-header-content">
        <div class="jw-mobile-text">
Random Definitions                </div>
</span>
</div>


<button type="button" class="jw-mobile-menu__button jw-mobile-toggle" aria-label="Toggle menu">
<span class="jw-icon-burger jw-icon-burger--cross"></span>
</button>
</div>
<header class="header-wrap js-topbar-content-container">
<div class="header-wrap__inner">
<div class="jw-header-logo">
<div class="jw-header jw-header-title-container jw-header-text jw-header-text-toggle" data-stylable="false">
<h1 id="jw-header-title" class="jw-header-title">
Random Definitions    </h1>
</div>
</div>
</div>
</header>
<div id="jw-slideshow" class="jw-slideshow jw-slideshow-toggle jw-slideshow--height-ratio banner-md" data-pause="7000" data-autoplay="1" data-transition="horizontal" data-ratio="0.8">
<div class="bx-wrapper"><div class="bx-viewport">
<ul>
<li class="jw-slideshow-slide">
<div data-key="0" data-text="Example text" data-subtext="Enter text here" data-buttontext="" data-buttontarget="_self" data-backdrop="1" data-layout="no-text" style="background-position: 50% 50%; background-image: url('https://primary.jwwb.nl/unsplash/ggeZ9oyI-PE.jpg?enable-io=true&amp;fit=bounds&amp;width=1920&amp;height=1920');" data-background-position-x="0.5" data-background-position-y="0.5" class="jw-slideshow-slide-content jw-slideshow-slide-content--display-cover jw-slideshow-slide-content--backdrop ">                            <div class="jw-slideshow-slide-backdrop"></div>
<div class="bx-caption-wrapper jw-slideshow-slide-align-center" style="opacity: 0;">
<div class="bx-caption">
<div class="jw-slideshow-title">Example text</div>
            </div>
</div>
</div>
</li>

</ul>
</div></div>
<div class="jw-slideshow__scroll-arrow">
<i class="website-rendering-icon-down-open-big"></i>
</div>
</div>


<nav class="jw-menu-copy">
</nav>
<div class="main-content">

<main class="block-content">
<div data-section-name="content" class="jw-section jw-section-content jw-responsive">
<div id="jw-element-435093190" data-jw-element-id="435093190" class="jw-tree-node jw-element jw-strip-root jw-tree-container">
<div id="jw-element-435093191" data-jw-element-id="435093191" class="jw-tree-node jw-element jw-strip jw-tree-container jw-strip--default jw-strip--style-color jw-strip--color-default jw-strip--padding-both jw-node-is-first-child jw-strip--primary jw-node-is-last-child">
<div class="jw-strip__content-container"><div class="jw-strip__content jw-responsive">
<div id="jw-element-435097024" data-jw-element-id="435097024" class="jw-tree-node jw-element jw-contact-form jw-node-is-first-child">
<form method="POST" class="jw-form-container" id="myForm">                                    
<div class="jw-element-form-group"><label for="jwFormeySHYO_dynamic-form-3495856-12097783" class="jw-element-form-label">term (optional)</label>
<div class="jw-element-form-content"><input type="text" name="dynamic-form-3495856-12097783" id="jwFormeySHYO_dynamic-form-3495856-12097783" class="form-control jw-element-form-input-text" bind:value={termValueName}>
<input type="button" class="jw-element-form-offset jw-btn jw-btn--size-small"  value="Reset form" onclick={resetForm}>

</div></div>                                                
     
                   <div class="hidden"><label for="jwFormjchqS1_captcha" class="jw-element-form-label">Leave this field empty</label><div class="jw-element-form-content"><input type="text" name="captcha" id="jwFormjchqS1_captcha" class="form-control jw-element-form-input-text" value=""></div></div>        
                   <input type="hidden" name="csrf_3495856" id="jwFormzbBISy_csrf_3495856" value="I8xSBMo0jJMHeLyp">                        
<div class="jw-element-form-group">
<input type="button" class="jw-element-form-offset jw-btn jw-btn--size-small" onclick={getData} value="Request Definition">

</div>
</form></div>
<div id="jw-element-435097122" data-jw-element-id="435097122" class="jw-tree-node jw-element jw-button">
</div>
<div id="jw-element-435097147" data-jw-element-id="435097147" class="jw-tree-node jw-element jw-spacer">
<div class="jw-element-spacer-container " style="height: 50px">
</div>
</div><div id="jw-element-435104926" data-jw-element-id="435104926" class="jw-tree-node jw-element jw-image-text">
<div class="jw-element-imagetext-text">
<h2><strong>Definition:</strong></h2>    </div>
</div><div id="jw-element-435097154" data-jw-element-id="435097154" class="jw-tree-node jw-element jw-image-text jw-node-is-last-child">
{#if invalidResponse}
    <div class="jw-element-imagetext-text">
        <p><strong>Failed to request term {termValueName}</strong></p>
    </div>
{:else}
    <div class="jw-element-imagetext-text">
        <p><strong>word:</strong></p>
        <p>{currentWord()}</p>
        <p><strong>definition:</strong></p>
        <p>{currentDefinition()}</p>
        <p><strong>example:</strong></p>
        <p>{currentExample()}</p>   
    </div>
{/if}


</div></div></div></div></div>            </div>
<div class="jw-element-spacer-container " style="height: 50px">
</div>
<div class="jw-element-spacer-container " style="height: 50px">
</div>
<div class="jw-element-spacer-container " style="height: 50px">
</div>
</main>
</div>


<footer class="block-footer">
    <div data-section-name="footer" class="jw-section jw-section-footer jw-responsive">
                <div class="jw-strip jw-strip--default jw-strip--style-color jw-strip--primary jw-strip--color-default jw-strip--padding-both"><div class="jw-strip__content-container"><div class="jw-strip__content jw-responsive">            <div id="jw-element-435093189" data-jw-element-id="435093189" class="jw-tree-node jw-element jw-simple-root jw-tree-container jw-tree-container--empty">
    </div>                            <div class="jw-credits clear">
                    <div class="jw-credits-owner">
                        <div id="jw-footer-text">
                            <div class="jw-footer-text-content">
                                                            </div>
                        </div>
                    </div>
                    <div class="jw-credits-right">
                                                <div id="jw-credits-tool">

    </div>
                </div>
            </div>
                </div></div></div>    </div>
</footer>

<div class="jw-mobile-bar-container hidden"></div></div>
<div class="jw-bottom-bar__spacer">
        <div class="jw-website-spacer jw-website-spacer--jump-to-editor"></div>
<div class="jw-website-spacer jw-website-spacer--mobile-bar hidden"></div></div>

        <div id="jw-variable-loaded" style="display: none;"></div>
        <div id="jw-variable-values" style="display: none;">
                                <span data-jw-variable-key="background-color" class="jw-variable-value-background-color"></span>
                                <span data-jw-variable-key="background" class="jw-variable-value-background"></span>
                                <span data-jw-variable-key="font-family" class="jw-variable-value-font-family"></span>
                                <span data-jw-variable-key="paragraph-color" class="jw-variable-value-paragraph-color"></span>
                                <span data-jw-variable-key="paragraph-link-color" class="jw-variable-value-paragraph-link-color"></span>
                                <span data-jw-variable-key="paragraph-font-size" class="jw-variable-value-paragraph-font-size"></span>
                                <span data-jw-variable-key="heading-color" class="jw-variable-value-heading-color"></span>
                                <span data-jw-variable-key="heading-link-color" class="jw-variable-value-heading-link-color"></span>
                                <span data-jw-variable-key="heading-font-size" class="jw-variable-value-heading-font-size"></span>
                                <span data-jw-variable-key="heading-font-family" class="jw-variable-value-heading-font-family"></span>
                                <span data-jw-variable-key="menu-text-color" class="jw-variable-value-menu-text-color"></span>
                                <span data-jw-variable-key="menu-text-link-color" class="jw-variable-value-menu-text-link-color"></span>
                                <span data-jw-variable-key="menu-text-font-size" class="jw-variable-value-menu-text-font-size"></span>
                                <span data-jw-variable-key="menu-font-family" class="jw-variable-value-menu-font-family"></span>
                                <span data-jw-variable-key="menu-capitalize" class="jw-variable-value-menu-capitalize"></span>
                                <span data-jw-variable-key="website-size" class="jw-variable-value-website-size"></span>
                                <span data-jw-variable-key="footer-text-color" class="jw-variable-value-footer-text-color"></span>
                                <span data-jw-variable-key="footer-text-link-color" class="jw-variable-value-footer-text-link-color"></span>
                                <span data-jw-variable-key="footer-text-font-size" class="jw-variable-value-footer-text-font-size"></span>
                                <span data-jw-variable-key="content-color" class="jw-variable-value-content-color"></span>
                                <span data-jw-variable-key="accent-color" class="jw-variable-value-accent-color"></span>
                                <span data-jw-variable-key="footer-color" class="jw-variable-value-footer-color"></span>
                                <span data-jw-variable-key="menu-color" class="jw-variable-value-menu-color"></span>
                        </div>
                    </div>


<style>
    .jw-slideshow-slide-content {
        min-height: 80vh;
    }
    @media screen and (min-height: 1200px) {
        .jw-slideshow-slide-content {
            min-height: 960px;
        }
    }
    .jw-slideshow-slide-content { padding-top: 0px; padding-bottom: 0px; } 
    .jw-background {
        background-color: #d2d2d2 !important
    }
</style>