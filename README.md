# DPB

Projeto Java (Maven + JUnit 5) com pipeline Jenkins acionado por webhook do GitHub.

## Estrutura

```
dpb/
├── .devcontainer/devcontainer.json
├── src/
│   ├── main/java/com/dpb/model/Item.java
│   └── test/java/com/dpb/model/ItemTest.java
├── .gitignore
├── Jenkinsfile
├── pom.xml
└── README.md
```

## Rodar localmente

```
mvn clean test
```

## Configurar o webhook

**No Jenkins**
1. Instale os plugins: Git, GitHub, Pipeline.
2. Em Manage Jenkins > Tools, cadastre `Maven3` (Maven) e `JDK21` (JDK).
3. Crie um job do tipo Pipeline (ou Multibranch Pipeline) com "Pipeline script from SCM", apontando para este repositório e o arquivo `Jenkinsfile`.
4. No job, marque "GitHub hook trigger for GITScm polling" (no Pipeline o `githubPush()` do Jenkinsfile já cobre isso após a primeira execução manual).

**No GitHub** (Settings > Webhooks > Add webhook)
- Payload URL: `http://SEU_JENKINS:8080/github-webhook/` (a barra final é obrigatória)
- Content type: `application/json`
- Evento: `Just the push event`

Se o Jenkins roda na sua máquina, exponha-o com ngrok ou similar, pois o GitHub precisa alcançar a URL.
