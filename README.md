# Mini-App de Verificação World ID

Este é um mini-aplicativo React que implementa a verificação de humanidade usando World ID (worldcoin.org) como porta de entrada para o projeto principal NFT BNB.

## Sobre o Projeto

Este mini-app serve como uma "prova de humanidade" através da tecnologia de leitura de íris do World ID. Após a verificação bem-sucedida, o usuário é redirecionado para o projeto principal hospedado na Vercel.

## Tecnologias Utilizadas

- React + TypeScript
- Vite
- @worldcoin/idkit (SDK oficial do World ID)

## Configuração para Desenvolvimento

1. Clone este repositório
2. Instale as dependências:
   ```bash
   pnpm install
   ```
3. Inicie o servidor de desenvolvimento:
   ```bash
   pnpm run dev
   ```

## Configuração do World ID

Para usar este aplicativo em produção, você precisa:

1. Criar uma conta no [Worldcoin Developer Portal](https://developer.worldcoin.org)
2. Criar um novo aplicativo e obter seu `app_id`
3. Criar uma nova ação e obter seu `action_id`
4. Substituir os IDs de exemplo no arquivo `src/App.tsx`:

```typescript
<IDKitWidget
  app_id="seu_app_id_aqui" // Substitua pelo seu app_id
  action="sua_action_id_aqui" // Substitua pela sua action_id
  onSuccess={onSuccess}
  handleVerify={handleVerify}
  verification_level={VerificationLevel.Orb}
>
```

## Deploy no Render.com

### Pré-requisitos

- Uma conta no [Render.com](https://render.com)
- Seu código enviado para um repositório Git (GitHub, GitLab, etc.)

### Passos para Deploy

1. Faça login na sua conta do Render.com
2. Clique em "New" e selecione "Static Site"
3. Conecte seu repositório Git
4. Configure o deploy com as seguintes informações:
   - **Nome**: world-id-verification (ou outro nome de sua escolha)
   - **Branch**: main (ou a branch que contém seu código)
   - **Build Command**: `pnpm install && pnpm run build`
   - **Publish Directory**: `dist`
5. Clique em "Create Static Site"

### Configuração de Ambiente (Opcional)

Se você quiser manter seus IDs do World ID como variáveis de ambiente:

1. No painel do seu site no Render.com, vá para "Environment"
2. Adicione as variáveis:
   - `VITE_WORLD_APP_ID`: seu app_id do World ID
   - `VITE_WORLD_ACTION_ID`: sua action_id do World ID

E então modifique o código para usar essas variáveis:

```typescript
<IDKitWidget
  app_id={import.meta.env.VITE_WORLD_APP_ID || "app_staging_d5c9c71a1c9b2b0a9b3c8b9e9c8d7e6f"}
  action={import.meta.env.VITE_WORLD_ACTION_ID || "human-verification"}
  // ...resto do código
>
```

## Integração com o Projeto Principal

Após o deploy, você pode integrar este mini-app como porta de entrada para seu projeto principal:

1. Configure seu domínio personalizado no Render.com (opcional)
2. Atualize a URL de redirecionamento no arquivo `src/App.tsx` para apontar para seu projeto principal:

```typescript
const onSuccess = () => {
  console.log("Verificação bem-sucedida!");
  setVerificationSuccess(true);
  
  // Atualize esta URL para seu projeto principal
  setTimeout(() => {
    window.location.href = "https://nft-bnb-20250527.vercel.app/";
  }, 2000);
};
```

## Observações Importantes

- Este mini-app usa um ID de aplicativo de teste do World ID. Para produção, você deve substituir pelo seu próprio ID.
- A verificação atual é simulada para fins de demonstração. Em um ambiente de produção, você deve implementar a verificação no backend conforme a documentação do World ID.
- O redirecionamento está configurado para o projeto principal na Vercel. Atualize a URL conforme necessário.

## Recursos Adicionais

- [Documentação do World ID](https://docs.world.org/world-id/quick-start/installation)
- [Documentação do Render.com](https://render.com/docs)
