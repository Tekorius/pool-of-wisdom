# FOSOauthBundle

## Install and config

`Symfony 4.1` - `June 2018`

### 1. Require the bundle

        composer require friendsofsymfony/oauth-server-bundle

### 2. Create the following entities

#### src/Entity/OAuthAccessToken.php

    <?php

    namespace App\Entity;

    use FOS\OAuthServerBundle\Entity\AccessToken as BaseAccessToken;
    use Doctrine\ORM\Mapping as ORM;

    /**
     * @ORM\Entity
     * @ORM\Table(name="oauth_access_token")
     * @ORM\AttributeOverrides({
     *     @ORM\AttributeOverride(name="token",
     *         column=@ORM\Column(
     *             name = "token",
     *             length = 191,
     *             unique = true
     *         )
     *     )
     * })
     */
    class OAuthAccessToken extends BaseAccessToken
    {
        /**
         * @ORM\Id
         * @ORM\Column(type="integer")
         * @ORM\GeneratedValue(strategy="AUTO")
         */
        protected $id;

        /**
         * @ORM\ManyToOne(targetEntity="App\Entity\OAuthClient")
         * @ORM\JoinColumn(nullable=false)
         */
        protected $client;

        /**
         * @ORM\ManyToOne(targetEntity="App\Entity\User")
         * @ORM\JoinColumn(name="user_id", referencedColumnName="id", onDelete="CASCADE")
         */
        protected $user;
    }

#### src/Entity/OAuthAuthCode.php

    <?php

    namespace App\Entity;

    use FOS\OAuthServerBundle\Entity\AuthCode as BaseAuthCode;
    use Doctrine\ORM\Mapping as ORM;

    /**
     * @ORM\Entity
     * @ORM\Table(name="oauth_auth_code")
     * @ORM\AttributeOverrides({
     *     @ORM\AttributeOverride(name="token",
     *         column=@ORM\Column(
     *             name = "token",
     *             length = 191,
     *             unique = true
     *         )
     *     )
     * })
     */
    class OAuthAuthCode extends BaseAuthCode
    {
        /**
         * @ORM\Id
         * @ORM\Column(type="integer")
         * @ORM\GeneratedValue(strategy="AUTO")
         */
        protected $id;

        /**
         * @ORM\ManyToOne(targetEntity="App\Entity\OAuthClient")
         * @ORM\JoinColumn(nullable=false)
         */
        protected $client;

        /**
         * @ORM\ManyToOne(targetEntity="App\Entity\User")
         * @ORM\JoinColumn(name="user_id", referencedColumnName="id", onDelete="CASCADE")
         */
        protected $user;
    }

#### src/Entity/OAuthClient.php

    <?php

    namespace App\Entity;

    use FOS\OAuthServerBundle\Entity\Client as BaseClient;
    use Doctrine\ORM\Mapping as ORM;

    /**
     * @ORM\Entity
     * @ORM\Table(name="oauth_client")
     */
    class OAuthClient extends BaseClient
    {
        /**
         * @ORM\Id
         * @ORM\Column(type="integer")
         * @ORM\GeneratedValue(strategy="AUTO")
         */
        protected $id;
    }

#### src/Entity/OAuthRefreshToken.php

    <?php

    namespace App\Entity;

    use FOS\OAuthServerBundle\Entity\RefreshToken as BaseRefreshToken;
    use Doctrine\ORM\Mapping as ORM;

    /**
     * @ORM\Entity
     * @ORM\Table(name="oauth_refresh_token")
     * @ORM\AttributeOverrides({
     *     @ORM\AttributeOverride(name="token",
     *         column=@ORM\Column(
     *             name = "token",
     *             length = 191,
     *             unique = true
     *         )
     *     )
     * })
     */
    class OAuthRefreshToken extends BaseRefreshToken
    {
        /**
         * @ORM\Id
         * @ORM\Column(type="integer")
         * @ORM\GeneratedValue(strategy="AUTO")
         */
        protected $id;

        /**
         * @ORM\ManyToOne(targetEntity="App\Entity\OAuthClient")
         * @ORM\JoinColumn(nullable=false)
         */
        protected $client;

        /**
         * @ORM\ManyToOne(targetEntity="App\Entity\User")
         * @ORM\JoinColumn(name="user_id", referencedColumnName="id", onDelete="CASCADE")
         */
        protected $user;
    }

### 3. Configure security.yaml

Add this to your `security.yaml` file

    security:
        firewalls:
            oauth_token:
                pattern: ^/oauth/v2/token
                security: false
            oauth_authorize:
                pattern: ^/oauth/v2/auth
                # Havent figured this out yet... for now use anonymous
                anonymous: true
            api_doc:
                pattern: ^/api/doc
                security: false
            api:
                pattern: ^/api
                fos_oauth: true
                stateless: true

        access_control:
            - { path: ^/api, roles: [ IS_AUTHENTICATED_FULLY ]}

### 4. Import bundle routes

Append the following lines to `config/routes.yaml`

    fos_oauth_server_token:
        resource: "@FOSOAuthServerBundle/Resources/config/routing/token.xml"

    fos_oauth_server_authorize:
        resource: "@FOSOAuthServerBundle/Resources/config/routing/authorize.xml"

### 5. Configure the bundle

Since the package doesn't have a Flex recipe, you need to create
`fos_oauth_server.yaml` file yourself.

Create `config/packages/fos_oauth_server.yaml` file and add the
following lines:

    fos_oauth_server:
        db_driver: orm
        client_class: App\Entity\OAuthClient
        access_token_class: App\Entity\OAuthAccessToken
        refresh_token_class: App\Entity\OAuthRefreshToken
        auth_code_class: App\Entity\OAuthAuthCode

        service:
            user_provider: App\Security\User\UserProvider

            options:
                supported_scopes:
                    myscope_1
                    myscope_2

### 6. Enable twig

You also need to enable twig. Open up `config/packages/framework.yaml`
and add this

    framework:
        templating:
            engines: ['twig']

### 6. Create a client

Using console:

    ./c fos:oauth-server:create-client --redirect-uri="" --grant-type="password"
