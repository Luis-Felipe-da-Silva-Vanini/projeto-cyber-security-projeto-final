# projeto-cyber-security-projeto-final
funcionamento de malware

📋 Estrutura do Repositório

Copy code
/README.md                 # Este arquivo com documentação completa
/ransomware/               # Pasta com scripts do Ransomware
  - ransomware.py          # Script principal para criptografia/descriptografia
  - chave.key              # Arquivo de chave gerado (exemplo)
/keylogger/                # Pasta com scripts do Keylogger
  - keylogger.py           # Script principal para captura de teclas
  - dados_capturados.txt   # Arquivo de saída (exemplo)
/images/                   # Capturas de tela (opcional)
  - print_ransomware.png   # Exemplo de execução
  - print_keylogger.png    # Exemplo de captura
/requirements.txt          # Dependências Python
🛠️ Configuração do Ambiente
Instale o Python 3.x (recomendado 3.8+).

Clone este repositório:


Copy code
git clone https://github.com/seu-usuario/simulacao-malwares.git
cd simulacao-malwares
Instale as dependências:


Copy code
pip install -r requirements.txt
cryptography para o Ransomware.
pynput para o Keylogger.
smtplib (já vem com Python) para envio de email.
Ambiente Seguro: Execute tudo em uma VM (VirtualBox ou VMware) com Kali Linux ou Ubuntu. Nunca em produção!

🔐 Ransomware Simulado
Como Funciona
O Ransomware simula o sequestro de arquivos: criptografa arquivos de teste (ex: .txt), deixa uma mensagem de "resgate" e permite descriptografia com a chave correta. Usa a biblioteca cryptography com Fernet (AES).

Arquivos de Teste
Crie arquivos de exemplo na pasta /ransomware/:

arquivo_teste.txt com conteúdo: "Este é um arquivo de teste."
Script: ransomware.py
python
61 lines
Copy code
Download code
Click to expand
from cryptography.fernet import Fernet
import os
...
Como Executar
Rode python ransomware.py para criptografar.
Verifique os arquivos: eles ficam ilegíveis.
Para descriptografar, descomente as linhas finais e rode novamente.
Resultado Esperado: Arquivos criptografados e mensagem de resgate criada. (Veja /images/print_ransomware.png para exemplo.)

⌨️ Keylogger Simulado
Como Funciona
O Keylogger captura teclas pressionadas, salva em um arquivo .txt e envia por email automaticamente. Usa pynput para captura e smtplib para envio.

Script: keylogger.py
python
55 lines
Copy code
Download code
Click to expand
from pynput.keyboard import Key, Listener
import smtplib
...
Como Executar
Configure as credenciais de email (use uma conta de teste).
Rode python keylogger.py.
Digite algo no teclado; pressione ESC para parar e enviar email.
Verifique dados_capturados.txt e o email.
Resultado Esperado: Teclas capturadas salvas e enviadas. (Veja /images/print_keylogger.png para exemplo.)

Nota: Para torná-lo "invisível", rode em background com python keylogger.py & no Linux, ou compile com PyInstaller.

🛡️ Como se Proteger
Antivírus e EDR: Use ferramentas como Malwarebytes ou Windows Defender para detectar comportamentos suspeitos.
Firewall: Bloqueie acessos não autorizados.
Sandboxing: Execute códigos suspeitos em VMs isoladas.
Conscientização: Não baixe anexos desconhecidos; use senhas fortes e 2FA.
Monitoramento: Verifique logs de sistema e rede.
Atualizações: Mantenha SO e apps atualizados.
Backup: Faça backups regulares para recuperar dados sem pagar resgate.
📚 Reflexões e Aprendizados
Este projeto mostrou como malwares exploram vulnerabilidades simples, como execução de scripts não verificados. Em cenários reais, eles causam danos enormes. O aprendizado reforça a importância de boas práticas: nunca execute códigos de fontes não confiáveis, e sempre teste em ambientes controlados. Se usado eticamente, isso ajuda a fortalecer defesas.
