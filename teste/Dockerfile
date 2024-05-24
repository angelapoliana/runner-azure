FROM alpine:latest
LABEL maintainer="Seu Nome <seuemail@example.com>"

# Adiciona um arquivo de texto simples
RUN echo "Olá, mundo!" > /app/teste.txt

# Define o diretório de trabalho
WORKDIR /app

# Exibe o conteúdo do arquivo de texto ao iniciar o contêiner
CMD cat teste.txt