# Cypress Snippets

title

```js
    describe('My First Test', () => {
    })
```

subtitle

```js
    it('finds the content "type"', () => {
    })
```

open link

```js
    cy.visit('https://example.cypress.io')
```

find first type word in page

```js
    cy.contains('type')
```

click on element or link

```js
    cy.get('#pass_btn').click()
```

page address should include /commands/actions

```js
    cy.url().should('include', '/commands/actions')
```

Get an input by class, type into it

```js
    cy.get('.action-email').type('fake@email.com')
```

Verify that the value has been updated

```js
    cy.get('.action-email').should('have.value', 'fake@email.com')
```

get element by specific attribute and value

```js
    cy.get('[data-testid="action-email"]')
```

after clicking on element wait 2000 ms then input element should be visible

```js
    cy.get('#submit_btn').click().wait(2000).then(()=>{
        cy.get('#url_input').should('be.visible')
    })
```

give value of input and going to that url

```js
    cy.get('#url_input').invoke('val').then((inputValue) => {
        const modifiedUrl = `${inputValue}`;
        cy.visit(modifiedUrl)
    });
```

log 

```js
    cy.log(modifiedUrl);
```

## Code Coverage

cmd

```bash
    npm i @cypress/code-coverage
```
cypress/support/e2e.js

```js
    import '@cypress/code-coverage/support'

    import { defineConfig } from 'cypress'
    import coverageTask from "@cypress/code-coverage/task";
    // import '@cypress/code-coverage/support'

    export default defineConfig({
    // setupNodeEvents can be defined in either
    // the e2e or component configuration
    e2e: {
        setupNodeEvents(on, config) {
        coverageTask(on, config);
        // include any other plugin code...

        // It's IMPORTANT to return the config object
        // with any changed environment variables
        return config
        },
    },
    })
```