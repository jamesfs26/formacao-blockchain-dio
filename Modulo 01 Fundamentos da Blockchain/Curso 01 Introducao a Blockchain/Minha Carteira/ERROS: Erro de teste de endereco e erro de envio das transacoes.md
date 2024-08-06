Fiz um Desafio de Projeto proposto pela DIO dentro do Bootcamp Binance - Blockchain Developer with Solidity

A proposta do projeto era criar sua primeira carteira (wallet) para Criptomoedas, entretanto essa não era uma carteira real para movimentar moedas com valores reais e sim uma carteira Testnet para movimentar moedas sem valor como é o caso da Bitcoin Faucet.

A ideia deste projeto é aprender didaticamente de forma segura sobre a funcionalidade do mercado Cripto, como funciona uma transação na blockchain na prática em contraste com o que já foi aprendido no conteúdo teorico, como enviar e receber transações em uma blockchain, como funciona uma carteira digital para Criptos.

A ideia do projeto era criar por meio da Electron Testnet a carteira, e testar por meio do site: blockchain.com testar o endereço da carteira conforme feito pelo professor em aula.

A primeira etapa foi criar por meio do Node.js a carteira.
Na segunda etapa deveria ser feito o teste de endereço da carteira para fins de checagem por meio dos recursos de teste da Blockchain.com.
Na terceira etapa a ideia era receber e enviar moedas sem valor para a carteira de teste para aprender na prática como são feitas as movimentações e transações no sistema de blocos e movimentações na carteira de Criptos.

A etapa de criação da carteira foi realizada com êxito. Entretanto o teste de endereço na Blockchain conforme mostrado em aula não foi possível de ser realizado, a alegação do site é de que não reconhece o endereço fornecido da carteira criada. Pelo mesmo motivo a etapa de transação (envio e recebimento de criptos) também falhou.

Com ajuda de alguns alunos do curso consegui resolver a etapa de verificação, porém, o método deles falhava na Bitcoin Faucet, então pedi para o Chat GPT gerar um código válido de uma Carteira Testnet para uso na Bitcoin Faucet, e essa solução me salvou. Consegui vincular o endereço ao Electron e fazer os procedimentos de transação.

Vou deixar o código aqui em baixo, para caso algum aluno tenha a mesma dificuldade.

### Código para Gerar a carteira

// Importando as dependências
const bip32 = require('bip32');
const bip39 = require('bip39');
const bitcoin = require('bitcoinjs-lib');

// Definir a rede [bitcoin = rede principal (mainnet) / testnet = rede de teste (testnet)]
const network = bitcoin.networks.testnet;

// Derivação de Carteiras HD
const path = "m/49'/1'/0'/0";

// Gerar a frase mnemônica
let mnemonic = bip39.generateMnemonic();
const seed = bip39.mnemonicToSeedSync(mnemonic);

let root = bip32.fromSeed(seed, network);

// Criando uma conta - Par Pvt-Pub Keys
let account = root.derivePath(path);
let node = account.derive(0).derive(0);

let btcAddress = bitcoin.payments.p2wpkh({
    pubkey: node.publicKey,
    network: network,
}).address;

console.log("Carteira Gerada");
console.log("Endereço: ", btcAddress);
console.log("Chave Privada:", node.toWIF());
console.log("Seed:", mnemonic);
