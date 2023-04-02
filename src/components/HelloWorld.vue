<template>
  <div class="hello">
    <h1>Mi Secreto: {{ secret }}</h1>
    <p>
      Ejemplo utilizando AWS Secret Manager mediante Cognito Identity provider.
    </p>
    <small>
      <p>
        <strong>Héctor Fernández</strong>
      </p>
      <p>AWS Community Builder</p>
    </small>
  </div>
</template>

<script>
import { CognitoIdentityClient } from "@aws-sdk/client-cognito-identity";
import { fromCognitoIdentityPool } from "@aws-sdk/credential-providers";
import {
  SecretsManagerClient,
  GetSecretValueCommand,
} from "@aws-sdk/client-secrets-manager";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      secret: undefined,
    };
  },
  async created() {
    try {
      const region = "us-east-1"; // Cambia esto a la región donde está configurado tu recurso de Secret Manager
      const identityPoolId = "us-east-1:fgfg89vb-66vf-439e-fgf9-fdfgfdgfdg99"; // Cambia esto a tu ID de Identity Pool
      const tempCredentials = fromCognitoIdentityPool({
        client: new CognitoIdentityClient({ region }),
        identityPoolId,
        clientConfig: { region },
      });

      const client = new SecretsManagerClient({
        region,
        credentials: tempCredentials,
      });

      const paramsSecretManager = {
        SecretId:
          "arn:aws:secretsmanager:us-east-1:06548457975:secret:dev/google_maps_apikey-kMap2w",
      };

      const data = await client.send(
        new GetSecretValueCommand(paramsSecretManager)
      );

      this.secret = data.SecretString;
    } catch (err) {
      console.error(err);
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
