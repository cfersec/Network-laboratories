# Mapeamento de Rede com Nmap

## Objetivo
Identificar dispositivos ativos na rede local, portas abertas e serviços em execução, utilizando a ferramenta Nmap a partir de uma máquina virtual.

## Ferramentas Utilizadas
- Nmap  
- Sistema operacional Linux (Kali Linux - máquina virtual)

## Procedimento
Inicialmente, foi identificado o endereço IP da máquina virtual (Kali) utilizando o comando:

<img width="249" height="53" alt="image" src="https://github.com/user-attachments/assets/47e28227-4495-4b01-beed-73d9eeaddee5" /><br>



Foi retornado o endereço IPv4 "192.168.0.22", pertencente à rede local.

Em seguida, foi realizado um scan para descoberta de hosts ativos na rede:

<img width="367" height="54" alt="image" src="https://github.com/user-attachments/assets/ed321ed1-8c55-4fa6-99ac-d17be8b8eaf3" />


Esse comando permitiu identificar os dispositivos ativos na mesma rede da máquina virtual.

Após a identificação dos hosts, foi selecionada a máquina principal da rede como alvo (`192.168.0.11`) para uma análise mais detalhada.

O scan de portas foi realizado com o comando:

<img width="1119" height="368" alt="image" src="https://github.com/user-attachments/assets/a72e15a6-d00f-4c49-a85a-32d12d947bee" />


---

## Resultados Observados

### Descoberta de Hosts
O scan identificou 9 hosts ativos na rede local, incluindo:

- 192.168.0.1 (roteador)
- 192.168.0.11 (máquina principal - alvo do scan)
- Outros dispositivos identificados por fabricante (Samsung, TP-Link, entre outros)

A identificação dos fabricantes foi possível através da análise do endereço MAC (OUI).

---

### Scan da Máquina Principal (Alvo)
Ao escanear a máquina principal com firewall desativado, foram identificadas as seguintes portas abertas:

- 135/tcp – msrpc  
- 139/tcp – netbios-ssn  
- 445/tcp – microsoft-ds  

Essas portas estão associadas a serviços do sistema operacional Windows, principalmente relacionados à comunicação interna e compartilhamento de arquivos (SMB).

---

### Observação sobre a Máquina Virtual
Durante os testes, também foi realizado um scan na VM(Kali), porem não foram identificadas portas abertas:

<img width="764" height="174" alt="image" src="https://github.com/user-attachments/assets/db15e18e-7cf9-4cdc-afcf-508d0be1c63e" />



Esse comportamento aponta a ausência de serviços expostos ou presença de mecanismos de proteção.

---

## Análise
A utilização de uma máquina virtual como origem do scan permitiu observar como um host dentro da rede pode mapear outros dispositivos e identificar serviços ativos.

Foi possível identificar padrões comuns de sistemas Windows, especialmente relacionados a portas utilizadas para comunicação interna e compartilhamento de recursos.

O uso do parâmetro `-Pn` permitiu realizar o scan independentemente de respostas ICMP, sendo útil em cenários onde o ping pode estar bloqueado.

Além disso, a análise evidenciou a diferença entre hosts com serviços expostos e hosts sem exposição de portas, como no caso da máquina virtual.

---

## Conclusão
O laboratório demonstrou como um dispositivo dentro da rede pode identificar outros hosts ativos e mapear serviços disponíveis através de suas portas.

A utilização da máquina virtual como ponto de origem do scan permitiu simular um cenário comum de análise interna, enquanto a observação da máquina principal evidenciou padrões reais de serviços em execução em sistemas Windows.






