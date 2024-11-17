## Sonar: como rodar localmente

### Setup

1. Instale o JDK mais recente de https://www.oracle.com/cis/java/technologies/downloads/ 

2. Baixe o SonarScanner de https://docs.sonarsource.com/sonarqube/9.9/analyzing-source-code/scanners/sonarscanner/

3. Ajuste o PATH do macOS para incluir o SonarScanner:

	1. Edite o arquivo de configuração do zsh:

		```bash
		nano ~/.zshrc
		```

	 2. Adicione o caminho do `bin`  do SonarScanner com a linha:

		```bash
		export PATH="/Users/seu_usuario/Downloads/sonar-scanner-<versão>/bin:$PATH"
		```

		Salve o arquivo: `CTRL + O`

		Saia do arquivo: `CTRL+ X`

		3. Atualize o terminal:

		```bash
		source ~/.zshrc
		```

		4. Verifique a instalação:

		```bash
		sonar-scanner --version
		```

4. Permita a execução do Java (se ele foi bloqueado) em Preferências do Sistema > Segurança e Privacidade.

### Configurando o projeto

1. Adicione o SonarScanner ao projeto:

	```bash
	npm install --save-dev sonar-scanner
	```

2. Adicione um script no `package.json`:

	```json
	"scripts": {
	  "sonar": "sonar-scanner"
	}
	```

3. Crie o arquivo de configuração na raiz do projeto (neste exemplo usando Sonar cloud):

	```bash
	touch sonar-project.properties
	```

	```properties
	sonar.organization=[sua organization]
	sonar.projectKey=[sua project key]
	sonar.projectName=[seu projeto]
	sonar.projectVersion=1.0
	sonar.language=ts
	sonar.sources=src
	sonar.tests=src
	sonar.test.inclusions=src/**/*.spec.ts
	sonar.host.url=https://sonarcloud.io
	sonar.token=[seu token]
	```

4. Execute o SonarScanner:

	```bash
	npm run sonar
	```

### Usando SonarQube localmente

1.  Instale o Docker Desktop se não tiver. No terminal, execute:

	```bash
	docker run -d --name sonarqube -p 9000:9000 sonarqube
	```

2. Acesse http://localhost:9000 com usuário e senha `admin` (será solicitado trocar no primeiro acesso) e crie o projeto local;

3. Altere o token no arquivo `sonar-project.properties`, remova a linha de `organization` e altere a url para:

	```properties
	sonar.host.url=http://localhost:9000
	```

4. Execute o SonarScanner:

	```bash
	npm run sonar
	```

	
