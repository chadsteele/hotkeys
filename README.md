# How to add HotKeys in React
So, I was looking for this for longer than it took to write and so, I thought I'd better share it.

Usage...

```javascript
        <HotKey keys={["ArrowUp"] }>
           <SomeClickableComponent />
        </HotKey>
```

Optional parameters [scope, callback]...

The default scope is the whole document and the default callback is to click the first child.  Keep in mind, you can map more than one key, since keys attribute accepts a string or an array of strings

```javascript
        <HotKey keys={["ArrowUp"] scope={window.document} callback={myfunc}>
           <SomeClickableComponent />
        </HotKey>
```

Here's the code...

```javascript
import React from 'react'
import { useEffect } from 'react'

export function HotKey(props){

    const scope = props.scope || window.parent
    useEffect(()=>{
        scope.addEventListener("keydown",onKeydown)
        return ()=>{
            scope.removeEventListener('keydown',onKeydown)
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

git [https://github.com/chadsteele/hotkeys](https://github.com/chadsteele/hotkeys)

doc [https://dev.to/chadsteele/how-to-add-hotkeys-in-react-4610](https://dev.to/chadsteele/how-to-add-hotkeys-in-react-4610)
