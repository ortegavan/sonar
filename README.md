## Sonar: como rodar localmente

### Setup

1. Instalar o JDK mais recente de https://www.oracle.com/cis/java/technologies/downloads/ 

2. Baixar o SonarScanner de https://docs.sonarsource.com/sonarqube/9.9/analyzing-source-code/scanners/sonarscanner/

3. Ajustar o PATH do macOS para incluir o SonarScanner:

	1. Editar o arquivo de configuração do zsh:

		```bash
		nano ~/.zshrc
		```

	 2. Adicionar o caminho do `bin`  do SonarScanner com a linha:

		```bash
		export PATH="/Users/seu_usuario/Downloads/sonar-scanner-<versão>/bin:$PATH"
		```

		Salvar o arquivo: `CTRL + O`

		Sair do arquivo: `CTRL+ X`

		3. Atualizar o terminal:

		```bash
		source ~/.zshrc
		```

		4. Verificar a instalação:

		```bash
		sonar-scanner --version
		```

4. Permitir a execução do Java (se ele foi bloqueado) em Preferências do Sistema > Segurança e Privacidade.

### Configuração do projeto

1. Adicionar o SonarScanner ao projeto:

	```bash
	npm install --save-dev sonar-scanner
	```

2. Adicionar um script no `package.json`:

	```json
	"scripts": {
	  "sonar": "sonar-scanner"
	}
	```

3. Criar o arquivo de configuração na raiz do projeto:

	```bash
	touch sonar-project.properties
	```

	```properties
	sonar.organization=ortegavan
	sonar.projectKey=ortegavan_recipes
	sonar.projectName=recipes
	sonar.projectVersion=1.0
	sonar.language=ts
	sonar.sources=src
	sonar.tests=src
	sonar.test.inclusions=src/**/*.spec.ts
	sonar.host.url=https://sonarcloud.io
	sonar.token=[seu token]
	```

4. Executar o SonarScanner:

	```bash
	npm run sonar
	```

	
