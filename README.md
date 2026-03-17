# 📱 Gestor de Finanças (Mobile CLI Edition)

Um sistema de gestão financeira desenvolvido em **Java** com interface de linha de comando (CLI) otimizada para terminais mobile. O grande diferencial deste projeto é que ele foi **100% desenvolvido, compilado e executado em um smartphone Android** utilizando o ambiente Termux.

## ✨ Funcionalidades
- Cadastro e listagem de **Receitas** e **Despesas**.
- Filtros por categoria (ex: lazer, mercado, salário) com validação de input ("Fail Fast").
- Relatórios mensais agrupados.
- **Interface Verticalizada:** Projetado em formato de "cards" para não quebrar a visualização na tela estreita do celular.
- Persistência de dados com **PostgreSQL** e **Hibernate/JPA**.

## 🚀 Tecnologias Utilizadas
- **Java 21**
- **Apache Maven** (Gerenciamento de dependências e build)
- **PostgreSQL** (Banco de dados relacional)
- **Hibernate / JPA** (Mapeamento Objeto-Relacional)
- **Git / GitHub** (Versionamento via SSH)
- **Termux** (Emulador de terminal Linux para Android)

---

## 🛠️ Como rodar este projeto no seu celular (Via Termux)

Se você quiser clonar e rodar este projeto no seu próprio dispositivo Android, siga o passo a passo abaixo.

### 1. Preparando o ambiente (Termux)
Primeiro, atualize os pacotes do seu terminal:
```bash
pkg update && pkg upgrade -y
```
### Instalando o Git para clonar o repositório
```bash
pkg install git -y
```
### Instalando o Java 21
```bash
pkg install openjdk-21 -y
```
### Instalando o Maven
```bash
pkg install maven -y
```
### Instalando o PostgreSQL
```bash
pkg install postgresql -y
```

### Inicializando o cluster do banco de dados
```bash
initdb $PREFIX/var/lib/postgresql
```
### Iniciando o servidor do banco de dados
```bash
pg_ctl -D $PREFIX/var/lib/postgresql start
```

## Criando usuário no banco de dados
### entre no console do banco

```bash
psql postgres
```
Dentro do console do PostgreSQL (postgres=#), crie o seu usuário, conceda a
permissão para criar bancos de dados e crie o banco do projeto:

```bash
SQL
-- Cria o usuário com uma senha segura
CREATE USER seu_usuario WITH PASSWORD 'sua_senha_aqui';

-- Dá permissão para o usuário criar novos bancos de dados (CREATEDB)
ALTER ROLE seu_usuario CREATEDB;

-- Cria o banco de dados do projeto pertencente ao usuário criado
CREATE DATABASE financas OWNER seu_usuario;

-- Sai do console interativo do PostgreSQL
\q
```
## Clone o repositório via SSH

```bash
git clone git@github.com:Azevd0/Gestor-de-Financas-mobile-.git
```
## Insira as credenciais do seu banco de dados no persistence.xml
```bash
<property name="jakarta.persistence.jdbc.driver" value="org.postgresql.Driver" />
			<property name="jakarta.persistence.jdbc.url"
				value="jdbc:postgresql://localhost:5432/seu_database" /> <!-- ALTERE DE ACORDO COM A SUA CONFIGURACAO -->
			<property name="jakarta.persistence.jdbc.user" value="seu_usuario" /> <!-- ALTERE DE ACORDO COM A SUA CONFIGURACAO -->
			<property name="jakarta.persistence.jdbc.password" value="sua_senha" /> <!-- ALTERE DE ACORDO COM A SUA CONFIGURACAO -->
```

## Estrutura do projeto
```bash
Gestor-de-Financas/JAVA/
│
├── pom.xml                
├── dependency-reduced-pom.xml 
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/br/financas/       
│   │   │       │
│   │   │       ├── dao/             
│   │   │       │   ├── DespesaDao.java   
│   │   │       │   └── ReceitaDao.java   
│   │   │       │
│   │   │       ├── entity/       
│   │   │       │   ├── Despesa.java       
│   │   │       │   └── Receita.java  
│   │   │       │
│   │   │       ├── main/           
│   │   │       │   └── App.java          
│   │   │       │
│   │   │       ├── menu/            
│   │   │       │   └── Menu.java          
│   │   │       ├── service/           
│   │   │       │   └── FinanceiroService.java 
│   │   │       │
│   │   │       └── util/              
│   │   │           └── JpaUtil.java      
│   │   │
│   │   └── resources/
│   │       └── META-INF/
│   │           └── persistence.xml 
│   │
│   └── test/              
│
└── target/               
    ├── classes/           
    └── app.jar <- O executável final da aplicação
```

### Execute a aplicação com o comando:
```bash
java -jar app.jar
```
