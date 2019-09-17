# ESLint
## Install Library
```
sudo npm i -g eslint
```

## Initial Project
```
eslint init
```

## Auto Fix Your Project
```
eslint --fix src/backend/libs/*.js
```

## Rules
- Unexpected `await` inside a loop.
  - push all promise result into an array and use Promise.all
- Unexpected use of continue statement.
  - use if
- Unary operator '++' used.
  - use += 1
- Expected an error object to be thrown.
  - use new Error()
- Variable is assigned a value but never used.
  - remove unused variable
- Unexpected console statement.
  - use this.logger.log or this.logger.debug
- Redundant use of `await` on a return value.
  - just return
