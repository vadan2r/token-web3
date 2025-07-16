# token-web3
Projeto DIO Criando o Seu Primeiro Token do Zero nos Padrões Web3

# Criando seu Primeiro Token Web3 (ERC-20) do Zero

Este guia passo a passo ensinará como criar seu próprio token ERC-20, implantá-lo na rede de teste Sepolia e interagir com ele usando a MetaMask.

## Pré-requisitos

*   **Node.js e npm (Node Package Manager):**  Certifique-se de ter o Node.js instalado. npm geralmente vem com o Node.
*   **Metamask:**  Instale a extensão Metamask no seu navegador.
*   **Um Editor de Texto:** (VS Code, Sublime Text, etc.)

## Passo 1: Configurando a Metamask para Sepolia

1.  **Instale a Metamask:** Se ainda não o fez, instale a extensão Metamask no seu navegador.

2.  **Crie ou Importe uma Carteira:** Siga as instruções da Metamask para criar uma nova carteira ou importar uma existente.  ***Guarde sua frase secreta em um local seguro!***

3.  **Adicione a Rede Sepolia:**

    *   **Opção 1: Adicionar Automaticamente (Recomendado):**
        *   Vá para [Chainlist](https://chainlist.org/).
        *   Conecte sua Metamask ao Chainlist.
        *   Procure por "Sepolia" e clique em "Add to Metamask".
        *   Aprove a adição da rede na Metamask.

    *   **Opção 2: Adicionar Manualmente:**
        *   Abra a Metamask e clique no menu de seleção de rede (onde diz "Ethereum Mainnet", "Sepolia" ou algo similar).
        *   Clique em "Add a network" (Adicionar rede).
        *   Clique em "Add a network manually" (Adicionar uma rede manualmente).
        *   Preencha os detalhes da rede:
            *   **Network Name:** Sepolia
            *   **New RPC URL:**  (Você pode usar um RPC público como `https://rpc.sepolia.org`, mas para maior confiabilidade, use um serviço como QuickNode ou Alchemy, veja abaixo.)
            *   **Chain ID:** 11155111
            *   **Currency symbol:** SepoliaETH
            *   **Block Explorer URL (optional):** [https://sepolia.etherscan.io](https://sepolia.etherscan.io)
        *   Clique em "Save" (Salvar).

4.  **Obtenha SepoliaETH (ETH de Teste):**
    *   É *essencial* ter SepoliaETH para pagar as taxas de gás (custo de transação) para implantar e interagir com seu contrato.
    *   Use um dos seguintes faucets (observe que alguns podem exigir um saldo mínimo na Mainnet - se encontrar um que exija, tente outro):
        *  [https://faucet-sepolia.rockx.com/](https://faucet-sepolia.rockx.com/)
        *   Pesquise no Google por "Sepolia ETH faucet" para encontrar mais opções.
    *   Cole o endereço da sua carteira Metamask no faucet e solicite ETH.
    *   Verifique se o SepoliaETH aparece no seu saldo da Metamask (pode demorar alguns minutos).

## Passo 2: Configurando um Endpoint RPC (Opcional, mas recomendado para estabilidade)

Para interagir de forma confiável com a rede Sepolia, você pode usar um serviço como QuickNode ou Alchemy para obter um endpoint RPC dedicado. Esses serviços fornecem uma infraestrutura mais estável e escalável do que usar RPCs públicos.

1.  **Crie uma Conta no QuickNode ou Alchemy:**
    *   Vá para [https://www.quicknode.com/](https://www.quicknode.com/) ou [https://www.alchemy.com/](https://www.alchemy.com/) e crie uma conta.

2.  **Crie um Endpoint Sepolia:**
    *   Siga as instruções do QuickNode ou Alchemy para criar um novo endpoint (nó) conectado à rede Sepolia.  Geralmente, você pode escolher um plano gratuito para testes.

3.  **Copie a URL do Endpoint RPC:**
    *   Após criar o endpoint, copie a URL HTTPS ou WSS do RPC.  Esta URL é o seu endpoint privado para a rede Sepolia.

4.  **Configure a Metamask com a URL do RPC:**
    *   Siga as instruções da seção anterior ("Adicione a Rede Sepolia") para *editar* a rede Sepolia na Metamask e substituir a "New RPC URL" pela URL do seu endpoint QuickNode ou Alchemy.  Isso garantirá que sua Metamask esteja se comunicando com a rede Sepolia através do seu endpoint privado.

## Passo 3: Criando o Código do Contrato Inteligente (Smart Contract)

Agora, vamos criar o código do contrato inteligente para o seu token ERC-20.

1.  **Abra um Editor de Texto:** (VS Code, Sublime Text, etc.)

2.  **Crie um Novo Arquivo:** Chame-o de `MyToken.sol`.

3.  **Cole o Código do Contrato:** Cole o seguinte código Solidity no arquivo `MyToken.sol`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor(string memory name, string memory symbol) ERC20(name, symbol) {
        _mint(msg.sender, 1000000 * 10 ** decimals()); // Mint 1,000,000 tokens para o criador
    }
}


## Passo 4: Implantando o Contrato Inteligente com Remix IDE

Acesse o Remix IDE: Vá para https://remix.ethereum.org/.

Crie um Novo Arquivo: No Remix, crie um novo arquivo chamado MyToken.sol.

Cole o Código: Cole o código do seu contrato (MyToken.sol) no Remix.

Compile o Contrato:
  Na aba "Solidity Compiler", selecione a versão do compilador que corresponde à versão especificada no seu código (0.8.0 ou superior).
  Clique em "Compile MyToken.sol". Se houver erros, corrija-os.

Implante o Contrato:
  - Na aba "Deploy & Run Transactions":
  - Defina o "Environment" para "Injected Provider - Metamask". Isso permite que o Remix use sua Metamask.
  - Certifique-se de que a rede Sepolia está selecionada na sua Metamask.
  - No campo "Contract", selecione MyToken - contracts/MyToken.sol.
  - Preencha os parâmetros do construtor:
  name: O nome do seu token (ex: "My Awesome Token")
  symbol: O símbolo do seu token (ex: "MAT")
  - Clique em "Deploy".
  - A Metamask abrirá uma janela solicitando a confirmação da transação. Revise os detalhes (especialmente a taxa de gás) e clique em "Confirm".

Aguarde a Implantação:
  - Aguarde a transação de implantação ser confirmada na rede Sepolia. Você pode verificar o status no explorador de blocos da Sepolia (sepolia.etherscan.io) usando o hash da transação fornecido pela Metamask.

## Passo 5: Interagindo com o Token na Metamask

Obtenha o Endereço do Contrato: Após a implantação bem-sucedida, o Remix exibirá o endereço do contrato. Copie este endereço.

Adicione o Token à Metamask:
  - Abra a sua Metamask.
  - Certifique-se de estar conectado à rede Sepolia.
  - Clique em "Import tokens" (Importar tokens).
  - Selecione a aba "Custom Token" (Token Personalizado).
  - Cole o endereço do contrato no campo "Token address" (Endereço do token).
  - A Metamask deve preencher automaticamente os campos "Token symbol" (Símbolo do token) e "Decimals of precision".
  - Clique em "Add Custom Token" (Adicionar token personalizado).
  - Clique em "Import Tokens" (Importar Tokens).

Verifique Seu Saldo: Agora você deve ver o seu token (ex: "MAT") e o saldo de 1.000.000 tokens na sua Metamask.

Observação: Este é um guia básico. A criação de tokens em um ambiente de produção requer mais considerações de segurança e otimização. Use este guia apenas para fins de aprendizado e teste.
