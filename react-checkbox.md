### React Checkbox
Dinamically switches orientation based on viewport, amount of checkboxes as well as lenght of text in each checkbox.

#### JSX

```jsx
import React, { useState, useRef, useEffect } from 'react'
import _ from './style.module.scss'
import Icon from '../Icon'

export interface Types {
	label?: string,
	checked?: boolean,
	selected?: boolean,
}

export default ({ label, checked, selected }: Types) => {
	const [Checked, check] = useState(checked)
	const [Selected, select] = useState(selected)

	return (
		<div role="checkbox" className={`${_.checkbox} ${Checked ? _.checked : ''} `} onClick={() => check(!Checked)}>
		 <div><Icon name={Selected ? 'minus' : 'tick'} /></div><span className={_.label}>{label}</span>
		</div>
	)
}

export const Group = ({ children, label, description }) => {
	const [column, setColumn] = useState(false)
	const parent = useRef(null)

	useEffect(() => {
		const element = parent.current
		element.querySelectorAll('span').forEach(span => span.textContent.length > 50 ? setColumn(true) : '')
	}, [parent])

	return (
		<section className={_.checkboxGroup}>
		 <span>{label}</span>
		  <div ref={parent} className={children.length > 3 || column ? _.column : ''}>
			 {children}
		  </div>
		 <small>{description}</small>
	  </section>
	)
}
```

#### SCSS
```css
.checkbox {
	display: flex;
	color: var(--charcoal60);
	cursor: pointer;
	transition: all .25s ease;
	div {
		width: 1rem;
		height: 1rem;
		min-width: 1rem;
		min-height: 1rem;
		border-radius: 3px;
		border: 2px solid var(--charcoal40);
		position: relative;
		margin: 0 .5rem 0 0;
		svg {
			opacity: 0;
			visibility: hidden;
			color: var(--charcoal100);
			position: absolute;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
		}
	}
	span {
		user-select: none;
		display: flex;
		align-items: center;
	}
	&.checked {
		color: var(--charcoal100);
		div {
			border-color: var(--charcoal100);
			background-color: var(--charcoal100);
			svg {
				opacity: 1;
				visibility: visible;
				color: white;
			}
		}
	}
}

.checkboxGroup {
	> span {
		margin: 0 0 1.68rem 0;
		display: block;
		color: var(--charcoal60);
		font-size: .875rem;
		@media (min-width: 48em) {
			margin: 0 0 .875rem 0;
		}
	}
	div {
		display: inline-flex;
		flex-direction: column;
		@media (min-width: 64em) {
			flex-direction: row;
		}
		&.column {
			flex-direction: column !important;
		}
		.checkbox {
			display: flex;
			flex-direction: row !important;
			margin: 0 1.5rem 1.25rem 0;
			line-height: 1.75rem;
			@media(min-width: 48em) {
				margin: 0 1.5rem .5rem 0;
				white-space: nowrap;
				align-items: center;
			}
			> div {
				margin: .35rem .5rem 0 0;
				@media(min-width: 48em) {
					margin: 0 .5rem 0 0;	
				}
			}
			&:last-of-type{
				margin: 0 0 .5rem 0;
			}
		}
	}
	small {
		display: block;
		margin: 1.18rem 0 0 0;
		font-size: .75rem;
		color: var(--red80);
		@media (min-width: 48em) {
			margin: 0.375rem 0 0 0;
		}
	}
}
```
