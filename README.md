# BuildInstaller

Script Cake que faz a etapa de atualização de um sistema(Branch) no servidor.

## Como usar
1. Abra o arquivo config.cake e preencha as configurações:
```
var branchPath = ""; // Caminho da Branch  ex: 05.19-sms1234567.8kjtrf
var systemName = ""; // Nome do sistema    ex: CORP_SMS1234567
var serverName = ""; // Nove do servidor   ex: BNU-JOAO
var systemUser = ""; // Usuário do sistema ex: treinamento
var systemPass = ""; // Senha do usuario do sistema
var wesPath    = ""; // (Opcional) Caminho onde o IIS aponta o site Ex: D:/Benner/Fontes/Corp/Produto/wes/WebApp/
```

2. Abra o programa PowerShell como Administrador.
3. Vá até a pasta onde está o arquivo build.ps1 desse projeto.
4. Se você deseja rodar uma atualização com todas as etapas basta digitar:
```
./build.ps1
```
5. Pronto!!!


## Etapas do script
Etapas que o script roda, você também pode executar cada etapa individualmente.
- **UpRunner:** Esta etapa habilita o sistema para fazer testes no ambiente Desktop/Runner, ela simplesmente agrupa as tasks "Tools", "BuilderArtifacts" e "ServerFiles".
```
./build.ps1 -target UpRunner
```
- **Tools:** Etapa onde são copiadas as ferramentas da Tec correspondentes à branch (Builder, BennerServer, ServerManager, Provider e Worker). O BennerServer precisa ser atualizado manualmente, caso tenha havido mudança de versão.
```
./build.ps1 -target Tools
```
- **BuilderArtifacts:** Faz uma cópia local dos XML's da estrutura, e em seguida é feita a atualização dos Artefatos de builder (mais informações em Observações no final desse Tutorial).
```
./build.ps1 -target BuilderArtifacts
```
- **ServerFiles:** Faz a cópia do Lote de servidor e de tecnologia, em seguida é feita a instalação destes lotes. 
```
./build.ps1 -target ServerFiles
```
- **UpWes:** Faz a cópia dos arquivos de Wes para a máquina e roda o migrate.
```
./build.ps1 -target UpWes
```
- **ConfigWes:** Faz a configuração do Wes (web.config)
```
./build.ps1 -target ConfigWes
```
- **WesArtifacts:** Instala os artefatos do Wes.
```
./build.ps1 -target WesArtifacts
```


- **ChangeToBranchDevelop:** Esta etapa altera a branch atual para a branch de desenvolvimento "develop".
```
./build.ps1 -target ChangeToBranchDevelop
```

- **GetMaxHandle:** Esta etapa obtém o identificador (handle) máximo da tabela especificada no banco de dados.
```
./build.ps1 -target GetMaxHandle
```

- **GenerateCSXFile:** Esta etapa gera um arquivo CSX com base nos arquivos de configuração fornecidos.
```
./build.ps1 -target GenerateCSXFile
```

- **GetCSXConteudo:** Esta etapa obtém o arquivo CSX de conteúdo.
```
./build.ps1 -target GetCSXConteudo
```

- **UpScriptBaseCSX:** Esta etapa atualiza o script base CSX com base nos arquivos fornecidos.
```
./build.ps1 -target UpScriptBaseCSX
```

- **UpScriptConteudoCSX:** Esta etapa atualiza o script de conteúdo CSX com base nos arquivos fornecidos.
```
./build.ps1 -target UpScriptConteudoCSX
```



## Observações
- Atualmente a instalação de artefatos do Wes pode não acontecer com sucesso em alguns casos:
  1. Quando precisa atualizar o provider oficial do servidor (vai dar erro na geração do CAC)
  2. Precisa copiar MANUALMENTE os binários de ServerFiles da pasta de instalação para \WebApp\Provider\Bin
