### Display Flickity slider only when more than one slide. 

```js
import Flickity from 'flickity';
(() => {
	if(document.querySelector('.BoxSlider')) {
		const boxSlider = document.querySelector('.BoxSlider'),
		      slides = boxSlider.querySelectorAll('.slide'),
					hasSlides = slides && slides.length > 1;

		if(hasSlides) {
			const flkty = new Flickity(boxSlider, {
				draggable: false,
				wrapAround: true,
				prevNextButtons: true,
				pageDots: true,
				adaptiveHeight: true,
				autoPlay: false,
				arrowShape: {
					x0: 5,
					x1: 60, y1: 50,
					x2: 60, y2: 0,
					x3: 60
				}
			});
		}
	}
})();
```
