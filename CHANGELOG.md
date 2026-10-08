# Changelog — Controle Financeiro (PWA)

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
