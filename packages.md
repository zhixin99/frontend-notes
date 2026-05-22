# Packages

## nanoid
A third party package that give us the id automatically
```jsx
import { nanoid } from "nanoid"

const [dice, setDice] = useState(generateAllNewDice())

function generateAllNewDice() {
    return new Array(10)
        .fill(0)
        .map(() => ({
            value: Math.ceil(Math.random() * 6), 
            isHeld: false,
            id: nanoid()
        }))
}
```

##