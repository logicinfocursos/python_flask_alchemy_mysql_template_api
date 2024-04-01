## api em python com flask / alchemy / mysql
<small>[link do projeto no github](https://github.com/logicinfocursos/python_flask_alchemy_mysql_template_api)</small>

Um template de api simples usando python com o framework flask e o orm alchemy acessando uma base de dados mysql.

Preparei um passo à passo com todas as etapas necessárias em ambiente windows (para linux e apple você precisará realizar alguns pequenos ajustes). 

Tenho certeza que seguindo as instruções abaixo, você conseguirá criar e executar a sua primeira api em python com flask e acessar a sua base de dados mysql.

Além do [mysql](https://docs.sqlalchemy.org/en/20/dialects/mysql.html), você pode usar o [postgreSQL](mysql://root:root@127.0.0.1:3306/aula) e [sqLite](https://docs.sqlalchemy.org/en/20/dialects/sqlite.html)

### ambiente necessário
[python 3](https://www.python.org/downloads/) qualquer versão do python à partir da versão 3.0
[vscode](https://code.visualstudio.com/download) ou outro editor de sua preferência
clintes de api [postman](https://www.postman.com/downloads/) ou [insomnia](https://insomnia.rest/download)
### criar e ativar o ambiente virtual (windows)
<pre>
C:\> mkdir api
C:\> cd api
C:\api> python -m venv venv
C:\api> venv\Scripts\activate.bat
(venv) C:\api> 
</pre>

### dependências para o projeto:
[flask](https://flask.palletsprojects.com/en/3.0.x/)
[flask-sqlalchemy](https://flask-sqlalchemy.palletsprojects.com/en/3.1.x/)
[mysql-connector-python](https://pypi.org/project/mysql-connector-python/)
[mysqlclient](https://pypi.org/project/mysqlclient/)
[flask-CORS](https://flask-cors.readthedocs.io/en/latest/)

### instalar as dependências do projeto:
Existem duas formas de você instalar as depências para esse projeto:
a) você pode usar o pip indicando cada dependência:
<pre>
(venv) C:\api> pip install flask mysqlclient mysql-connector-python
(venv) C:\api> pip install -U Flask-SQLAlchemy flask-cors
</pre>

b) ou você pode instalar as dependências através do arquivo "requirements.txt"
<pre>
(venv) C:\api> pip install -r requirements.txt
</pre>

Com as dependências instaladas, você pode gerar ou atualizar o arquivo requirements.txt
<pre>
(venv) C:\api> pip freeze > requirements.txt
</pre>

conteúdo arquivo "requirements.txt":
<pre>
Flask==3.0.2
Flask-Cors==4.0.0
Flask-SQLAlchemy==3.1.1
mysql-connector-python==8.3.0
mysqlclient==2.2.4
SQLAlchemy==2.0.29
</pre>
essas são as principais dependências, outras serão instaladas automaticamente a partir dessa lista inicial

### o alchemy cria as tabelas pra você no mysql
Ao executar o comando db.create_all(), o alchemy cria as tabelas relacionadas em classes com o argumento db.Model (class Usuario(db.Model)), mas se essa instrução ficar dentro código, a tabela usuario será sobrescrita sempre que a api for executada.

Para contonar isso, podemos usar o db.create_all() direto no prompt do python
<pre>
(venv) C:\api> python

Python 3.12.1 (tags/v3.12.1:2305ca5, Dec  7 2023, 22:03:25) [MSC v.1937 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
>>> from app import db
>>> db.create_all()
>>> ^Z + tecla enter (para sair o python)
</pre>

Com a tabela criada, basta inserir o código da api

### estrutura da tabela usuario
CREATE TABLE `usuario` (
	`id` INT(10) NOT NULL AUTO_INCREMENT,
	`nome` VARCHAR(50) NULL DEFAULT NULL COLLATE 'utf8mb4_unicode_ci',
	`email` VARCHAR(100) NULL DEFAULT NULL COLLATE 'utf8mb4_unicode_ci',
	PRIMARY KEY (`id`) USING BTREE
)
COLLATE='utf8mb4_unicode_ci'
ENGINE=InnoDB
AUTO_INCREMENT=1;

### string de conexão com o mysql:
mysql://user:senha-se-houver>@localhost-ou-a-url-do-server-mysql>:porta-opcional/nome-do-banco-de-dados

exemplo de preenchimento: 
mysql://root:root@127.0.0.1:3306/aula

### executar o projeto
<pre>
(venv) C:\api> python api.py
</pre>

no navegador:
http://127.0.0.1:5000/usuarios

Você terá um resultado semelhante a esse (com os dados que você inserir na tabela)
<pre>
// http://127.0.0.1:5000/usuarios

{
  "usuarios": [
    {
      "id": 1,
      "nome": "veronica",
      "email": "veronica@mail.com"
    }
  ],
  "mensagem": "ok"
}
</pre>

### extensões usadas no vscode
[Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
[Python Debugger](https://marketplace.visualstudio.com/items?itemName=ms-python.debugpy)
[Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
