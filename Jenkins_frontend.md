## SHELL-команды для сборки фронтенда в Jenkins ##

# Перейти в каталог frontend
cd frontend

# Установить nvm (если не установлен)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash

# Загрузить nvm в текущую сессию (если не сделано автоматически)
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion

# Установить и использовать Node.js 10.0.0
nvm install 10.0.0
nvm use 10.0.0

# Установить зависимости
npm install

# Собрать проект
npm run build
