# マスタリングイーサリアム第２章

Last edited time: April 2, 2023 9:24 AM

## **Ether Currency Units**

1 ETH=10^18 Wei

WeiはEthereumの最小単位であり、Ethereumにおける通貨単位の基本です。

Etherの単位名と名称には、

- 各単位
- 一般的な名前
- SI名

が与えられます。

| Value (in wei) | Exponent | Common name | SI name |
| --- | --- | --- | --- |
| 1 | 1 | wei | Wei |
| 1,000 | 10^3 | Babbage | Kilowei or femtoether |
| 1,000,000 | 10^6 | Lovelace | Megawei or picoether |
| 1,000,000,000 | 10^9 | Shannon | Gigawei or nanoether |
| 1,000,000,000,000 | 10^12 | Szabo | Microether or micro |
| 1,000,000,000,000,000 | 10^15 | Finney | Milliether or milli |
| 1,000,000,000,000,000,000 | 10^18 | Ether | Ether |
| 1,000,000,000,000,000,000,000 | 10^21 | Grand | Kiloether |
| 1,000,000,000,000,000,000,000,000 | 10^24 |  | Megaether |

## Choosing an Ethereum Wallet

- MetaMask、Jaxx、MyEtherWallet、Emerald Walletなどがある
- ウォレットはEthereumアカウントを管理するためのソフトウェアであり、キーを保持してトランザクションを作成・ブロードキャストできる
- Ethereumのプラットフォームはまだ改善中であり、様々なウォレットがあり、選択するのは困難である
- ウォレットアプリケーションはプライベートキーにアクセスできるため、信頼できるソースからのみダウンロードして使用する必要がある
- ポピュラーなウォレットアプリケーションほど信頼性が高い傾向がある
- ウォレットを変更することが簡単であり、古いウォレットから新しいウォレットに送金するか、プライベートキーをエクスポートして新しいウォレットにインポートするだけでよい

## Control and Responsibility

- Ethereumは分散システムであるため、ユーザーは自分自身のプライベートキーを制御する必要がある。
- プライベートキーを失うと、資金とコントラクトにアクセスできなくなるため、十分な注意が必要である。
- プライベートキーを安全に保管するためのいくつかのヒントがある：
    - セキュリティを即席で行わないこと
    - アカウントが重要であるほど高いセキュリティ手段を取ること
    - エアギャップデバイスから最高のセキュリティを得られる
    - プレーンフォームにプライベートキーを格納しないこと
        
        プレーンフォーム：特定のセキュリティ機能が付加されていない、基本的な形式のコンピューターシステム
        
    - プライベートキーを暗号化された形式で格納すること
    - パスワードを強力にすること
    - デジタルドキュメントにパスワードを保存しないこと
    - ニーモニックとしてキーのバックアップを作成すること
        
        ニーモニック：プライベートキーを復元するための単語のリスト。このリストを安全な場所に保管することで、プライベートキーを失った場合でもアクセスできるようになる。ニーモニックは通常、24語または12語のリストで構成され、ランダムに選択された単語が含まれる。
        
    - 大量の送金を行う前に、小額のテストトランザクションを行うこと
    - 新しいアカウントを作成する場合、最初に新しいアドレスに小さなテストトランザクションを送信すること
    - 公開ブロックエクスプローラーを使用する場合は、プライバシーに影響することに注意すること
        
        公開ブロックエクスプローラー：Ethereumのブロックチェーン上で発生したトランザクションやブロック、アドレスなどを閲覧することができるウェブサイトであり、誰でもアクセスして閲覧することができる。
        

## **Introducing the World Computer**

- Ethereumは分散型の世界コンピューターであるため、暗号通貨としての役割はその一部にすぎない。
- Etherは、スマートコントラクトを実行するための支払いに使用される。
- スマートコントラクトは、Ethereum仮想マシン（EVM）と呼ばれるエミュレートされたコンピューター上で実行されるコンピュータープログラムである。
- EVMはグローバルシングルトンであり、世界中のあらゆる場所で実行される単一インスタンスコンピューターのように動作する。
    - （ちなみにプログラミングにおける）シングルトン：単一のインスタンスしか持たないオブジェクト。このオブジェクトは、グローバルにアクセス可能であるため、プログラム内のどこからでもアクセスできる。

## **Externally Owned Accounts (EOAs) and Contracts**

- MetaMaskのウォレットに作成したアカウントは「外部所有アカウント（EOA）」であり、プライベートキーを持つことによって資金やコントラクトへのアクセスを制御できる。
- 「コントラクトアカウント」と呼ばれるもう一方のアカウントタイプは、スマートコントラクトコードを持つが、プライベートキーを持たない。
    
    スマートコントラクトコード：コントラクトアカウントの作成時にEthereumブロックチェーンに記録され、EVMによって実行されるソフトウェアプログラム。
    
- コントラクトアカウントは、トランザクションの宛先として指定されると、そのコントラクトが EVM 上で実行され、トランザクションとトランザクションデータが入力として使用される。
- トランザクションはether以外にもデータを含むことができ、そのデータには、実行するコントラクト内の特定の関数とその関数に渡すパラメーターを示すことができる。
- コントラクトアカウントはトランザクションを開始することはできないが、他のコントラクトを呼び出すことによってトランザクションに反応することができる。

## **A Simple Contract: A Test Ether Faucet**

- Solidityは最も一般的に使用されている
- faucetは、任意のアドレスにEtherを与えるものであり、定期的に再補充することができる

Example 1. Faucet.sol: A Solidity contract implementing a faucet

`link:code/Solidity/Faucet.sol[]`

| Note | You will find all the code samples for this book in the code subdirectory of https://github.com/ethereumbook/ethereumbook/. Specifically, our Faucet.sol contract is in:

code/Solidity/Faucet.sol |
| --- | --- |

```solidity
// SPDX-License-Identifier: CC-BY-SA-4.0

// Version of Solidity compiler this program was written for
pragma solidity 0.6.4;

// Our first contract is a faucet!
contract Faucet {
    // Accept any incoming amount
    receive() external payable {}

    // Give out ether to anyone who asks
    function withdraw(uint withdraw_amount) public {
        // Limit withdrawal amount
        require(withdraw_amount <= 100000000000000000);

        // Send the amount to the address that requested it
        msg.sender.transfer(withdraw_amount);
    }
}
```

- 簡単ながらも脆弱性があるコントラクトである
- SolidityはJavaScript、Java、C++などに似ている

コントラクトの定義

```solidity
contract Faucet {}
```

コントラクトのレシーブ関数

```solidity
receive () external payable {}
```

Etherの送金を受け取る関数であり、外部からEtherを受け取ることができる。

external: クラスの外からアクセスできる。 （アクセスの観点）

payable: ethを受け取ることができる。（つけてないとethは受け取れない）

コントラクトの関数

```solidity
withdraw(uint withdraw_amount) public {}
```

この関数は、コントラクトの出金制限を設定するために、

```solidity
require(withdraw_amount <= 100000000000000000);
```

のようにrequire関数を使って、1回の出金額を制限している。

出金処理は、

```solidity
msg.sender.transfer(withdraw_amount);
```

を使って行われる。ここで、msgオブジェクトは、すべてのコントラクトがアクセスできる入力の1つであり、トランザクションの送信元アドレスを表す。この関数で、指定されたアドレスにEtherを送金することができる。

## **Compiling the Faucet Contract**

- Solidityコンパイラを使用してSolidityコードをEVMバイトコードに変換する必要がある。
- 使いやすさを重視して、より一般的なIDEであるRemixを使用する。
    - [https://remix.ethereum.org](https://remix.ethereum.org/)

↓新しいファイルを追加

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_toolbar.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_toolbar.png)

↓コードを書く

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_faucet_load.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_faucet_load.png)

↓コンパイル

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_compile.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_compile.png)

Figure 13. Remix successfully compiles the Faucet.sol contract

エラーが発生するのであれば、Remix IDEが0.6以外のSolidityコンパイラのバージョンを使用している可能性が高い。その場合、pragmaディレクティブが_Faucet.sol_のコンパイルを防ぐ。

```
PUSH1 0x80 PUSH1 0x40 MSTORE CALLVALUE DUP1 ISZERO PUSH2 0x10 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP PUSH1 0xF4 DUP1 PUSH2 0x1F PUSH1 0x0 CODECOPY PUSH1 0x0 RETURN INVALID PUSH1 0x80 PUSH1 0x40 MSTORE PUSH1 0x4 CALLDATASIZE LT PUSH1 0x1F JUMPI PUSH1 0x0 CALLDATALOAD PUSH1 0xE0 SHR DUP1 PUSH4 0x2E1A7D4D EQ PUSH1 0x2A JUMPI PUSH1 0x25 JUMP JUMPDEST CALLDATASIZE PUSH1 0x25 JUMPI STOP JUMPDEST PUSH1 0x0 DUP1 REVERT JUMPDEST CALLVALUE DUP1 ISZERO PUSH1 0x35 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST POP PUSH1 0x5F PUSH1 0x4 DUP1 CALLDATASIZE SUB PUSH1 0x20 DUP2 LT ISZERO PUSH1 0x4A JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST DUP2 ADD SWAP1 DUP1 DUP1 CALLDATALOAD SWAP1 PUSH1 0x20 ADD SWAP1 SWAP3 SWAP2 SWAP1 POP POP POP PUSH1 0x61 JUMP JUMPDEST STOP JUMPDEST PUSH8 0x16345785D8A0000 DUP2 GT ISZERO PUSH1 0x75 JUMPI PUSH1 0x0 DUP1 REVERT JUMPDEST CALLER PUSH20 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF AND PUSH2 0x8FC DUP3 SWAP1 DUP2 ISZERO MUL SWAP1 PUSH1 0x40 MLOAD PUSH1 0x0 PUSH1 0x40 MLOAD DUP1 DUP4 SUB DUP2 DUP6 DUP9 DUP9 CALL SWAP4 POP POP POP POP ISZERO DUP1 ISZERO PUSH1 0xBA JUMPI RETURNDATASIZE PUSH1 0x0 DUP1 RETURNDATACOPY RETURNDATASIZE PUSH1 0x0 REVERT JUMPDEST POP POP JUMP INVALID LOG2 PUSH5 0x6970667358 0x22 SLT KECCAK256 STOP CODECOPY 0xDC DUP16 0xD SGT PUSH6 0xD2245039EDD7 RETURN CALLDATALOAD 0xC2 0xE4 SWAP9 0xF6 0x2C 0xF8 0xB3 OR JUMPDEST 0xAC 0xD8 CREATE2 SSTORE 0x4E SIGNEXTEND PUSH4 0x3164736F PUSH13 0x634300060C0033000000000000
```

## **Creating the Contract on the Blockchain**

- コントラクトをEthereumブロックチェーンに登録する必要がある
- コントラクトをブロックチェーンに登録するために、特別なトランザクションを作成し、宛先を0x0000000000000000000000000000000000000000に設定する必要がある（ゼロアドレス）
    
    ゼロアドレス：Ethereumブロックチェーン上で使用される特別なアドレス。このアドレスは、Ethereumブロックチェーン上で最初に生成されたアドレスであり、すべてのアカウントからアクセスできるため、トランザクションの宛先を指定するために使用される。ゼロアドレスにEtherを送信することはできませんが、このアドレスに送信することで、新しいアカウントを作成することができる。
    
- Remix IDEがトランザクションをMetaMaskに送信してくれる

↓Remix IDE のRunタブからデプロイすることができる

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_run.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_run.png)

↓トランザクションを構築するには、MetaMaskが承認が必要

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_metamask_create.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_metamask_create.png)

## **Interacting with the Contract**

### **Viewing the Contract Address in a Block Explorer**

“*ropsten.etherscan.io”* でコントラクトがどうなっているのか確認することができる。

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_contract_address.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_contract_address.png)

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/etherscan_contract_address.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/etherscan_contract_address.png)

### Funding the Contract

- コントラクトはまだ1つのトランザクションしか持っておらず、Etherも持っていない。
    - 作成トランザクションでコントラクトにEtherを送信しなかったためである。
- MetaMaskを使用してコントラクトにEtherを送信する必要がある。

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/metamask_send_to_contract.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/metamask_send_to_contract.png)

- コントラクトアドレスに対して関数が指定されていないトランザクションが送信された。
- デフォルト関数が呼び出され、これがペイアブルで宣言されていたため、1イーサがコントラクトの口座残高に入金された。
- コントラクトがEVM上で実行され、残高が更新された。

**Withdrawing from Our Contract**

- Faucetから資金を引き出すためには、withdraw関数を呼び出すトランザクションを構築する必要がある
- トランザクションには、withdraw_amount引数を渡す必要がある
- Remix IDEは、このトランザクションを作成し、MetaMaskで承認する
- Runタブのコントラクトを見ると、withdrawというオレンジ色のボックスが表示され、その下にuint256 withdraw_amountというフィールドが表示される

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_contract_interact.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_contract_interact.png)

- コントラクトで許可されている最大金額である0.1イーサを引き出したい。
- Ethereumの通貨価値は内部的にweiで表される。
- withdraw関数は、引き出し金額がweiで表されていることを想定している。
- 我々が必要とする金額は、100,000,000,000,000,000 wei（17桁の1）である。

Remixには、10^17のような大きな数を処理できないJavaScriptの制限がある。そのため、文字列として受け取り、大きな数として操作できるようにダブルクオートで囲む。クオートで囲まれていない場合、Remix IDEはそれを処理できず、「Error encoding arguments: Error: Assertion failed.”と表示される。

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_withdraw.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/remix_withdraw.png)

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/metamask_withdraw.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/metamask_withdraw.png)

MetaMaskのトランザクションで引き出し関数を呼び出す

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/etherscan_withdrawal_tx.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/etherscan_withdrawal_tx.png)

Etherscanはwithdraw関数を呼び出すトランザクションの確認

Internal Transactionsというタブが出現

この「内部トランザクション」は、*Faucet.sol*の`withdraw`関数からコントラクトによって送信された。

```
msg.sender.transfer(withdraw_amount);
```

↓EtherscanでコントラクトからEtherを転送する内部トランザクションを表示

![https://github.com/ethereumbook/ethereumbook/raw/develop/images/etherscan_withdrawal_internal.png](https://github.com/ethereumbook/ethereumbook/raw/develop/images/etherscan_withdrawal_internal.png)