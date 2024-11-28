```
            _____                     _____     _         
           |   __|___ ___ _ _ ___ ___|  _  |_ _| |___ ___     # Os: Ubuntu Server 24.04.1 LTS
           |__   | -_|  _| | | -_|  _|   __| | | |_ -| -_|    # Shell: bash 5.2.21 
           |_____|___|_|  \_/|___|_| |__|  |___|_|___|___|                                              
                                         |                              
                                     __| __|  _ \   __| _` |  _` |  _ \ 
                                   \__ \ |   (   | |   (   | (   |  __/ 
                                   ____/\__|\___/ _|  \__,_|\__, |\___| 
                                                            |___/       

```

# ServerPulse-storage
 
Este repositório foi projetado para armazenar, gerenciar e compartilhar arquivos. Ele é dividido em diferentes subdiretórios para facilitar a organização e o acesso aos dados.

## Estrutura do Diretório
- `/srv/projetos`: Contém os arquivos dos projetos em desenvolvimento.

- `/srv/backup`: Armazena cópias de segurança dos dados mais importantes.

- `/srv/temp`: Espaço temporário usado para transferência de arquivos.

- `/srv/compartilhamento`: Diretório de compartilhamento externo.
---
- `/home/usuario-admin`: Reservado para o usuario com maior cargo.

- `/home/usuario-viewer`: Usuario que vai apenas olhar. 
---
- `/tmp/arq-texto`: Quando precisa direcionar arquivos de texto para o principal.
  
- `/tmp/code`: Proprio para codigo, como se voce estivese dando commit.


## Funcionalidades

- `Scripts Automatizados`: Movimenta arquivos da pasta temporária para o diretório de compartilhamento.

- `Logs de Atividade`: Registra a atividade de arquivos para fins de monitoramento.

- `Backup Programado`: Realiza backups em intervalos regulares para maior segurança dos dados.



## Funcionalidade do tmp
A pasta tmp serve para ser como pasta temporaria servindo para deixar os arquivos nela e depois sendo retirecionado para outra pasta.
```bash
# Diretório de origem e destino
ORIGEM="/tmp"
DESTINO="/srv/compartilhamento"

# Verifica se o diretório de destino existe
if [ ! -d "$DESTINO" ]; then
    mkdir -p "$DESTINO"
fi

# Monitora novos arquivos na pasta de origem
inotifywait -m "$ORIGEM" -e create -e moved_to |
while read path action file; do
    # Move o arquivo para o diretório de destino
    mv "$path$file" "$DESTINO"
    echo "Arquivo $file movido para $DESTINO"
done
```
## Conetar servidor SAMBA

smb://IP_do_servidor/pasta_desejada
