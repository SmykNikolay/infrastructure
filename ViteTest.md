# Vite test

test: jest — запускает модульные тесты с помощью Jest.
test:watch: jest --watch — запускает тесты в режиме наблюдения за изменениями.
test:coverage: jest --coverage — собирает отчёт по покрытию тестами.
test:e2e: cypress run — запускает end-to-end тесты с помощью Cypress.

```json
{
  "scripts": {
    "test": "vitest run",
    "test:watch": "vitest",
    "test:coverage": "vitest run --coverage"
  }
}
```

vite.config.ts
```ts
/// <reference types="vitest" />
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react-swc';

export default defineConfig({
  plugins: [react()],
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: './src/setupTests.ts',
    coverage: {
      reporter: ['text', 'html'],
      exclude: [
        'node_modules/',
        'src/setupTests.ts',
      ]
    }
  }
});
```


## cypress
cypress.json
```json
{
  "baseUrl": "http://localhost:3000",
  "viewportWidth": 1280,
  "viewportHeight": 720,
  "video": false,
  "screenshotsFolder": "cypress/screenshots",
  "videosFolder": "cypress/videos",
  "integrationFolder": "cypress/integration"
}
```

example.spec.js
```js
describe('Example', () => {
  it('should work', () => {
    cy.visit('/');
    cy.get('button').click();
    cy.get('h1').should('have.text', 'Hello, world!');
  });
});
```

```json
{
  "scripts": {
    "test:e2e": "cypress run"
  }
}
```