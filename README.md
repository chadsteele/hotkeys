# How to add HotKeys in React
So, I was looking for this for longer than it took to write and so, I thought I'd better share it.

Usage...

```javascript
        <HotKey keys={["ArrowUp"]}>
           <SomeClickableComponent />
        </HotKey>
```

Here's the code...

```javascript
import React from 'react'
import { useEffect } from 'react'

export function HotKey(props){

    useEffect(()=>{
        window.document.addEventListener("keydown",onKeydown)
        return ()=>{
            window.document.removeEventListener('keydown',onKeydown)
        }
    })

    let keys = props.keys; // see https://keycode.info/
    if (!keys || !keys.length) return;
    if (typeof keys == 'string' || keys instanceof String) keys = [keys]

    const parent = React.createRef()
    const onKeydown = props.callback || ((e) => {
        if (keys.indexOf(e.code)>=0){
            parent?.current?.children?.[0]?.click()
            }      
    })

    return <div data-hotkey={props.keys} ref={parent}>
        {props.children}
    </div>

}

export default HotKey

```

documentation [dev.to](https://dev.to/chadsteele/hotkeys-in-react-3ej6-temp-slug-9005949/edit)
git [https://github.com/chadsteele/hotkeys](https://github.com/chadsteele/hotkeys)
