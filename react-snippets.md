## React Snippets
### React Hooks

Hooks are available only for function-based components, so they can't be used inside a class component.

#### useState

`react
import React, { useState } from 'react'

function UserComponent() {
  const [name, setName] = useState('John')
}
`
