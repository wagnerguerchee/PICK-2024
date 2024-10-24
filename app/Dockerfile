FROM cgr.dev/chainguard/python:latest-dev as dev
WORKDIR /app
# Criando um ambiente virtual no Python
RUN python -m venv venv
# Definindo o PATH para utilizar o ambiente virtual
ENV PATH="/app/venv/bin":$PATH
# Copiando e instalando dependências
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
# Segunda etapa (produção)
FROM cgr.dev/chainguard/python:latest
WORKDIR /app
# Copiando apenas o código necessário
COPY app.py .
COPY templates templates/
COPY static static/
# Copiando o ambiente virtual da primeira etapa
COPY --from=dev /app/venv /app/venv
# Definindo o PATH para utilizar o ambiente virtual na etapa final
ENV PATH="/app/venv/bin:$PATH"
# Expondo a porta da aplicação Flask
EXPOSE 5000
# Definindo o comando de inicialização da aplicação Flask
ENTRYPOINT ["python", "-m", "flask", "run", "--host=0.0.0.0", "--debug"]
