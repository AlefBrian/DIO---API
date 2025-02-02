# DIO---API
Como Fazer o Deploy de uma API na Nuvem na Prática

Este guia explica como desenvolver e fazer o deploy de uma API REST na nuvem utilizando Flask (Python) e o serviço AWS Elastic Beanstalk.

1. Configurar o Ambiente
Antes de iniciar, você precisará dos seguintes itens instalados:
Python 3.x
AWS CLI
AWS Elastic Beanstalk CLI
Git
Crie um ambiente virtual e instale as dependências:

python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate
pip install flask flask-restful boto3

2. Criar a API

Crie um arquivo app.py com o seguinte código:
from flask import Flask, jsonify, request
from flask_restful import Api, Resource

app = Flask(__name__)
api = Api(app)

class HelloWorld(Resource):
    def get(self):
        return jsonify({"message": "Hello, World!"})

api.add_resource(HelloWorld, '/')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)

    

from flask import Flask, jsonify, request
from flask_restful import Api, Resource

app = Flask(__name__)
api = Api(app)

class HelloWorld(Resource):
    def get(self):
        return jsonify({"message": "Hello, World!"})

api.add_resource(HelloWorld, '/')

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)

3. Criar os Arquivos Necessários

Crie um arquivo requirements.txt com as dependências:
flask
flask-restful
boto3

Crie um arquivo Procfile para indicar como rodar a aplicação:

web: gunicorn app:app

4. Criar e Configurar o Projeto na AWS

   Autentique-se na AWS CLI:
   aws configure
   eb init -p python-3.x api-deploy-tutorial

   Crie um ambiente de deploy:
   eb create api-deploy-env

   5. Fazer o Deploy da API

      Para enviar a aplicação para a AWS, use:
      eb deploy

      Para verificar o status:
      eb status

      Para acessar a URL do serviço:
      eb open

      6. Monitoramento e Logs

         Para visualizar logs:
         eb logs

         Para escalabilidade e gerenciamento, é possível configurar Auto Scaling e Load Balancer diretamente no console da AWS Elastic Beanstalk.

         7. Alternativa: Deploy no Heroku
        
         Se preferir usar o Heroku, siga os passos:

         heroku create api-deploy-tutorial
git init
git add .
git commit -m "Initial commit"
git push heroku master
heroku open
