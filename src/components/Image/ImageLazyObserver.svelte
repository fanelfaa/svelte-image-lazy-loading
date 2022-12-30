<script>
	/**
	 * @type {string}
	 */
	export let src;
	/**
	 * @type {string}
	 */
	export let alt;
	// observer options
	export let once = true;
	export let top = 0;
	export let bottom = 0;
	export let left = 0;
	export let right = 0;

	import { onMount } from 'svelte';

	/**
	 * @type {HTMLImageElement}
	 */
	let thisImage;

	let srcBlur =
		'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAP8AAADGCAMAAAAqo6adAAAAMFBMVEX////p6en8/PzS0tL5+fnx8fHn5+fX19f29vbt7e3a2trd3d3y8vLi4uL6+vru7u6sweb6AAAClElEQVR4nO3a3XarIBCGYSGgICr3f7cd0CZpfulea+vq5H3Ss3rAN4yj0XQdAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAOBDWJf7NBapz84evZyduXk4XRvncPSSdjSl073BH72snUzjmve2APHohe3CzkNxH3/4iBkQxmF11//m6KXtwQzfTjL2gy2CL8PwI7b/Ev9m3oc5H7SkPcVh6/7ZPfiv+gbwwyj55e/Jtd7qrkCod3vj8GLQqa7AvOZ/NefrPNxtQfsyY5LPq93vtgKorIAdU5LvO/O7w0p8jRUwqeRPb5Mp7QCbav6p4UiVBfCl/dO77i905p/r9j+67bmjsQDL3Lr9OvP7VArQ9oTDLvoK0KdZNGZanLr8El4q0HiwW5ZFV35Xdj+1PuCyrlTgvy5oZ6Hmb7j4V5JfKqCpAWr+5kfcNpQCfHB+F5Tln/4hv6YB8Nv+17b/kr//Vf6gK7/re8nf+oKr5A9BU34r8fu59Q2HU5e/M33ReHCNr+t9cKz52zJZhflDzd92A7y2v6bLn+zpegI0ndNB3+nfdbnmb7kCOK+v/dcrYFsDTELd9ssENKZpAgTvp8lr235pAFML8O47sJPdlwKo2/7aAKUCrx8BW9l9r3H71wYoFXh1YZP43uvcfjmz1wKY5x3g/KrpNcHfk7cCPJsBIedc4mvs/ipuBYiP+nuZYi5862PCP2jLb/p8OwXcFNf4WfMPoez3KdCbeLnFsc7nGLf8XuXsO/PmLEqrB/ms4Wv+mHWO/ishRvNTvMhqR9+F9eZnBeK5Auo3fyVToH/QAcrP/Gs23JwE0vmfk76yYYrSBuWTFX7dBQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDMF+dDFfFdX6/YAAAAAElFTkSuQmCC';

	onMount(() => {
		thisImage.src = srcBlur;
		if (typeof IntersectionObserver !== 'undefined') {
			const rootMargin = `${bottom}px ${left}px ${top}px ${right}px`;
			const observer = new IntersectionObserver(
				(entries) => {
					const intersecting = entries[0].isIntersecting;
					if (intersecting) {
						thisImage.src = src;
						thisImage.loading = 'eager';
					}
					if (intersecting && once) {
						observer.unobserve(thisImage);
					}
				},
				{
					rootMargin
				}
			);
			observer.observe(thisImage);
			return () => observer.unobserve(thisImage);
		}
	});
</script>

<img {src} {alt} width="200" height="200" bind:this={thisImage} loading="lazy" />

<style>
	img {
		object-fit: cover;
	}
</style>
