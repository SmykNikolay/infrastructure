
# Linting and Formatting

lint-staged: lint-staged — запускает линтеры для изменённых файлов перед коммитом.
lint: eslint src/**/*.{ts,tsx} — запускает ESLint для проверки кода.
lint:fix: eslint src/**/*.{ts,tsx} --fix — автоматически исправляет ошибки линтинга.
prettier:check: prettier --check src/**/*.{ts,tsx,css,scss} — проверяет форматирование кода с помощью Prettier.
prettier:write: prettier --write src/**/*.{ts,tsx,css,scss} — форматирует код с помощью Prettier.