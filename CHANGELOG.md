# Changelog — Controle Financeiro (PWA)

## 1.0.3 — estorno no cartão e ajuste da fatura (08/10/2026)

- **Estorno no cartão:** ao lançar uma **Receita**, escolha "Estorno no cartão (crédito na fatura)" na forma de pagamento — o valor entra como crédito na fatura (seguindo o lançamento e o fechamento) e reduz o limite usado. Se o estorno for maior que a fatura, o que sobrar abate a fatura seguinte. Não mexe no saldo das contas.
- **Ajustar fatura:** cada cartão ganha o botão **"Ajustar"** — escolha a fatura e informe o valor fechado do banco; o total passa a ser esse valor, sem apagar nem alterar os lançamentos. Informe de volta o valor calculado (ou deixe vazio) para voltar ao normal.
- Testes: 115 (`node --test`), todos passando.

## 1.0.2 — faturas de cartão pelas datas (08/10/2026)

- **Compras parceladas antigas não aparecem mais como atrasadas:** a fatura de cada compra segue a data do lançamento e o **fechamento** do cartão; o **vencimento** define o que ainda está em aberto. Faturas já vencidas (vencimento antes de hoje) são consideradas pagas automaticamente — ex.: compra em 25/06 num cartão que fecha dia 02 cai na fatura de julho e não conta como atraso.
- **A fatura atual continua em aberto**, com aviso de vencimento (ex.: "vence 10/10") — o app deixa de cobrar só o que já venceu.
- **Pagamentos abatem as faturas em aberto mais antigas**; um pagamento registrado para uma fatura já vencida fica com ela (não é contado duas vezes).
- Testes: 112 (`node --test`), todos passando.

## 1.0.1 — reconexão da nuvem sem recarregar a página (08/10/2026)

- **A sincronização não fica mais parada quando a sessão do Google expira** (~1 hora): o app renova a sessão antes de vencer (silenciosamente, quando o navegador permite); se não conseguir, mostra o cartão **“Continuar como…”** com um aviso — um toque reconecta e a sincronização volta sozinha. Antes, era preciso recarregar a página (F5) para as alterações aparecerem no outro aparelho.
- **CSP do login corrigida:** o estilo do cartão do Google (`accounts.google.com/gsi/style`) estava bloqueado pela política de segurança e podia impedir o cartão de aparecer. Também liberadas as imagens de avatar (`googleusercontent.com`) e as fontes (`fonts.gstatic.com`).
- Ao tentar sincronizar sem sessão válida (ex.: token vencido no meio do uso), a reconexão com um toque é disparada na hora, sem esperar o próximo ciclo.

## 1.0.0 — primeiro lançamento (08/10/2026)

Controle financeiro pessoal simples, privado e offline, para instalar no Windows, no Android e no navegador — com **nuvem opcional na sua própria conta Google**, cifrada de ponta a ponta.

- **Base:** derivado do **Finan+ web 1.2.0** (GPL-3.0-or-later, de Juscelino Be): núcleo financeiro, armazenamento criptografado (AES-256-GCM), PIN, assistente no aparelho, relatório em PDF, layout para computador e a nuvem com Apps Script.
- **Conta e nuvem (Ajustes):** entrar com o Google, ativar a sincronização (criar a **chave da casa** ou entrar com o código), status e "Sincronizar agora", **Membros**, **Código da casa**, "Enviar tudo daqui", "Apagar na nuvem" e "Desconectar".
- **Sincronização por registro, offline-first:** fila local que sobrevive a fechar o app; envio agrupado e leitura a cada ~15 s; conflitos avisam e a versão mais nova prevalece; exclusões viram lápide.
- **Serviço em `backend/appsscript/Code.gs`:** ações `hello`, `pull`, `push`, `members`, `member-add`, `member-remove` e `wipe`; a planilha é criada sozinha; `bootstrap()` define o administrador sem código de instalação. Guia completo em [NUVEM.md](NUVEM.md).
- **Ferramentas:** `npm run mock-cloud` (serviço de mentira com login simulado) e `npm run preview` (servidor estático próprio, sem depender do Python).
- **Testes:** 111 (`node --test`), todos passando.
