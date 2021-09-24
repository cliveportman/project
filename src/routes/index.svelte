<script>

  import Splash from '$lib/home/Splash.svelte'
  import Developer from '$lib/home/Developer.svelte'
  import Designer from '$lib/home/Designer.svelte'
  import Director from '$lib/home/Director.svelte'
  import Support from '$lib/home/Support.svelte'
  import Work from '$lib/home/Work.svelte'
  import Contact from '$lib/home/Contact.svelte'

  let active = 'home'
  function scroll(section) {
    let target = window[section]
		window.scrollTo({
			top: target.offsetTop,
			behavior: 'smooth'
		})

    gtag('event', 'section_view', {
      'event_label': section
    });

  }

  function updateActive(section) {
    active = section
  }

  $: console.log(active)

  const nav = [
    { section: 'home', title: 'Quick summary' },
    { section: 'developer', title: 'Quick summary' },
    { section: 'director', title: 'Quick summary' },
    { section: 'designer', title: 'Quick summary' },
    { section: 'support', title: 'Quick summary' },
    { section: 'work', title: 'Work' },
    { section: 'contact', title: 'Quick summary' }
  ]

</script>

<svelte:head>
	<title>Clive Portman - web/app developer, Norwich UK - craft cms, shopify, svelte</title>
</svelte:head>

<nav class="subnav" aria-label="Homepage only">
  {#each nav as link}
  <a href="#{link.section}" on:click|preventDefault="{ () => { scroll(link.section) } }" class="{link.section}" class:active="{active === link.section}">
    <span>{link.title}</span>
  </a>
  {/each}
</nav>


<Splash 
  on:intersect="{ (event) => {updateActive(event.detail.section)} }" 
  on:serviceClick="{ (event) => {scroll(event.detail.section)} }" 
/>
<Developer 
  on:intersect="{ (event) => {updateActive(event.detail.section)} }" 
/>
<Director
  on:intersect="{ (event) => {updateActive(event.detail.section)} }"
/>
<Designer 
  on:intersect="{ (event) => {updateActive(event.detail.section)} }"
/>
<Support 
  on:intersect="{ (event) => {updateActive(event.detail.section)} }"
/>
<Work 
  on:intersect="{ (event) => {updateActive(event.detail.section)} }"
/>
<Contact 
  on:intersect="{ (event) => {updateActive(event.detail.section)} }"
/>

<style lang="scss">

nav {

  position: fixed; bottom: 0; z-index: 9999;
  display: flex; width: 100%;

  @media (min-width: 600px) {
    bottom: calc(50% - 12.5rem); right: 0;
    width: 5rem;
    flex-direction: column;
  }

  a {
    display: block; width: calc(100vw / 6); height: calc(100vw / 6);
    position: relative;
    transition: border-width 1s;
    border: none; border-left: 0px solid transparent;
    line-height: calc(100vw / 6);
    font-size: 2rem;
    color: rgba(255,255,255,0.2);
    
    text-align: center;
    text-decoration: none;
    box-sizing: content-box;
    transition: transform 0.3s;

    &:hover:after {
        content: "◯";
    }

    @media (min-width: 600px) {
      width: 5rem; height: 5rem;
      line-height: 5rem;
    }

    span {
      display: none;
    }

    &.active:after {
        content: "⬤";
    }
  }

  .home { background: #036880; }
  .developer { background: #045C80; }
  .director { background: #024e80; }
  .designer { background: #233a59; }
  .support { background: #001d3d; }
  .work { background: #00152D; }
  .contact { background: #000D0D; }

}

</style>