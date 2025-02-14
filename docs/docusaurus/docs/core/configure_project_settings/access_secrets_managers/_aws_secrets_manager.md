import GxData from '../../_core_components/_data.jsx'
import PreReqFileDataContext from '../../_core_components/prerequisites/_file_data_context.md'

### Prerequisites {#prerequisites-aws}

- An AWS Secrets Manager instance.  See [AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/tutorials_basic.html).
- The ability to install Python packages with `pip`.
- <PreReqFileDataContext/>.

### Procedure {#procedure-aws}

1. Set up AWS Secrets Manager support.
   
   To use the AWS Secrets Manager with GX Core you will first need to install the `great_expectations` Python package with the `aws_secrets` requirement.  To do this, run the following command:

   ```bash title="Terminal"
   pip install 'great_expectations[aws_secrets]'
   ```

2. Reference AWS Secrets Manager variables in `config_variables.yml`.

   By default, `config_variables.yml` is located at: 'gx/uncomitted/config_variables.yml' in your File Data Context.

   Values in `config_variables.yml` that start with `secret|arn:aws:secretsmanager` will be substituted with corresponding values from the AWS Secrets Manager.  However, if the keywords following `secret|arn:aws:secretsmanager` do not correspond to keywords in AWS Secrets Manager no substitution will occur.

   You can reference other stored credentials within the keywords by wrapping their corresponding variable in `${` and `}`.  When multiple references are present in a value, the secrets manager substitution takes place after all other substitutions have occurred.

   An entire connection string can be referenced from the secrets manager.  In this example, `dev_db_credentials` is the Secret Name in AWS Secrets Manager, and `connection_string` is the Secret Key that corresponds to the value to be retrieved:

   ```yaml title="config_variables.yml"
    my_aws_creds:  secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|connection_string
   ```

   Or each component of the connection string can be referenced separately.  In these examples, `dev_db_credentials` remains the Secret Name in AWS Secrets Manager. However, rather than retrieving the value of the Secret Key `connection_string`, Secret Keys for individual parts of the connection string are provided for retrieval:
   
   ```yaml title="config_variables.yml"
    drivername: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|drivername
    host: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|host
    port: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|port
    username: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|username
    password: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|password
    database: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:dev_db_credentials|database
    ```

    Note that the last seven characters of an AWS Secrets Manager arn are automatically generated by AWS and are not mandatory to retrieve the secret. For example, the following two values retrieve the same secret:

   ```yaml title="config_variables.yml"
   secret1: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:my_secret-1zAyu6
   secret2: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:my_secret
   ```
   
3. Optional. Reference versioned secrets.

   Unless otherwise specified, the latest version of the secret is returned by default. To get a specific version of the secret you want to retrieve, specify its version UUID. For example:

   ```yaml title="config_variables.yml"
   versioned_secret: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:my_secret:00000000-0000-0000-0000-000000000000
   ```

4. Optional. Retrieve specific secrets from a JSON string.
 
   To retrieve a specific secret from a JSON string, include the JSON key after a pipe character `|` at the end of the secrets keywords.  For example:

   ```yaml title="config_variables.yml"
   json_secret: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:my_secret|<KEY>
   versioned_json_secret: secret|arn:aws:secretsmanager:${AWS_REGION}:${ACCOUNT_ID}:secret:my_secret:00000000-0000-0000-0000-000000000000|<KEY>
   ``` 