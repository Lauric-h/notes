# DevNotes   
   
## Count items with paginator   
```
{{ pagination.getTotalItemCount }}

```
## Get SQL prod dump   
- Launch Docker   
- `cd dev/decathlon-travel/dkt-infra-gcp && make tunnel-mysql-prod`   
- `cd dev/decathlon-travel/your-project && bin/import && bin/restore`   
- `Yes` then get SQL password from `.env.prod` and copy it   
   
## Make curL request with lots of redirects   
```
curl -L --max-redirs 500 -H "X-API-KEY: d8f559a25f01d6639276a48b2ad307b8" http://127.0.0.1:8000/api/export/stock

```
`-L` → follow redirects   
`--max-redirs` → set number of redirections   
`-H` custom header   
## Deploy specific feature   
- Have CLI gcloud https://cloud.google.com/sdk/docs/install   
- Have a running Docker   
- Being logged in gcloud   
   
`git checkout` on your feature branch.   
Run `FEATURE\_NAME=your-feature-name make deploy-feature`   
Configure docker if need be `gcloud auth configure-docker`   
If you need a composer token, set it:   
`FEATURE\_NAME=your-feature-name COMPOSER\_TOKEN=your-token make deploy-feature`   
## Get the selected option of select in JS   
```
const select = document.querySelector('select')
let text = select.options[select.selectedIndex].text
let value = select.options[select.selectedIndex].value 

```
## Get soft deleted entries from Symfony   
```
# In repository:
$filters = $this->_em->getFilters();
$filters->disable('softdeleteable');

return $this->createQueryBuilder('user')...

```
## Don’t render the rest of form Symfony   
```
{{ form_end(form, {render_rest: false}) }}

```
### Use datetime\_immutable in form   
```
'input' => 'datetime_immutable'

```
https://symfony.com/doc/current/reference/forms/types/datetime.html#input   
### Use assert   
```
use Symfony\Component\Validator\Constraints as Assert;

```
### Compute dates php   
```
// Diff between 2 dates
$date1->diff($date2)->days;

// Add
$date1->add(new \DateInterval('P' . $duration . 'D'));

// Subtract
$date1->sub(new \DateInterval('P' . $duration . 'D'));

```
⚠️ La manipulation de date modifie l’objet date, pour éviter d’avoir des problèmes, utiliser des `DateTimeImmutable`   
## Schema update avec dump sql   
```
# Dump le schema dans la console
symfony console doctrine:schema:update --dump-sql

```
## Extract   
```
/
  @paramclass-string<T>$className
  @parammixed$json
  @paramarray<string>|null$validationGroups
 
  @returnT
 
  @throwsApiFormException
  @template T of object
/
public function extract(string$className,$json, ?array$validationGroups= null, ?Closure$groupCallback= null)
{
    if ('' ===$json) {
        throw new ApiFormException(['No content provided']);
    }

$serializer= $this->getSerializer();

    try {
$object=$serializer->deserialize($json,$className, 'json');
    } catch (NotEncodableValueException|NotNormalizableValueException$exception) {
        throw new ApiFormException([$exception->getMessage()]);
    }
    if (null !==$groupCallback) {
$validationGroups=$groupCallback($validationGroups?? [],$object);
    }

/ @varValidatorInterface$validator/
$validator= $this->container->get('validator');
$violations=$validator->validate($object, null,$validationGroups);
    if (\count($violations) > 0) {
$errors= [];
        foreach ($violationsas$violation) {
$errors[$violation->getPropertyPath()] =$violation->getMessage();
        }

        throw new ApiFormException($errors);
    }

    return$object;
}

// Then use 
$data = $this->extract(Data::class, $this->getRequest()->getContent());

```
## Symfony deserialize into array of entity   
```
$data = $serializer->deserialize($request->getContent(), sprintf('%s[]', Data::class), 'json');

```
## SQL:  Export   
```
SELECT
    code,
    trs.name as sport,
    minprice_EUR as prix,
    duration as durée,
    practice as niveau,
    trd.name as pays,
    td.name as destination,
    tt.name as thème,
    CASE t.type WHEN 1 THEN 'gir' WHEN 2 THEN 'fit' END AS type
FROM travel_tours t
JOIN travel_tours__themes ttt on t.id = ttt.tour
LEFT JOIN travel_themes tt on ttt.theme = tt.id
JOIN travel_tours__referential_destinations ttrd on t.id = ttrd.tour
JOIN travel_referential_destinations trd on ttrd.referential_destination = trd.id
JOIN travel_tours__referential_sport ttrs on t.id = ttrs.tour
JOIN travel_referential_sport trs on ttrs.value_id = trs.id
JOIN travel_tours__destinations ttd on t.id = ttd.tour
JOIN travel_destinations td on ttd.destination = td.id
ORDER BY t.code


SELECT c.code, p.name as partner, s.name as sport, co.name as country,COUNT(distinct cd.id) as nb_dates,SUM(cd.remaining_stock) as total_remaining_stock
FROM circuit c
JOIN circuit_date cd on c.id = cd.circuit_id
LEFT JOIN partner p on c.partner_id = p.id
LEFT JOIN sport s on c.sport_id = s.id
LEFT JOIN country co on c.country_id = co.id
WHERE c.type = 'gir'
AND cd.departure_state != 'cancelled'
AND cd.departure_state != 'full'
AND cd.departure_date >= NOW()
GROUP BY c.code;

```
## Use ‘confirm’ JS in Twig   
```
<a href="link" onclick="return confirm('{{ 'text'|trans }}')"; >go to link</a>

```
## Catch different exceptions in same catch   
```
try {
 ...
} catch (FirstException | SecondException $e) {
 // handle $e
}

```
## Migration pour preprod   
faire un .env.preprod.local ⚠️ bdd commune à toutes les preprod   
lancer le funnel infra   
```
sfc —env=preprod d:m:m
// pour la prod
sfc —env=prod d:m:m

```
## Pluralization Twig   
```
'{0} Départ confirmé | {1} Encore %count% personne pour confirmer | ]1,Inf[ Encore %count% personnes pour confirmer'

```
## TESTS UNITAIRES   
- mock sert à fake le comportement des choses dont on a pas le contrôle absolu (mysql, api externes)   
- on ne teste que notre code, pas celui des autres → on mock   
   
## Twig raw filter on form   
On label you can use `label\_htm` in form type   
```
label_html => true

```
For choice in EnumType or ChoiceType, use `apply`   
```
// In messages.fr
key_trad:  'I want to use html in this sentence %s% this is a new line'

// twig template
{% apply replace({'%s%': '<br>'})
{{ form_widget(form.property) }}
{% endapply %}

```
## Descente db de prod vers la db de preprod   
- connect to tunnel prod   
- `bin/import` pour dl la db   
- connect to tunnel preprod   
- `bin/restore-preprod` pour upload la db dans la preprod   
- relancer les déploiement si migration dans les PR   
   
## Select la dernière version des circuit\_version par circuit   
```
SELECT
    c.code,
    cv.name
FROM circuit c
         JOIN (
    SELECT
        cv.circuit_id,
        MAX(cv.created_at) AS latest_created_at
    FROM circuit_version cv
    GROUP BY cv.circuit_id
) latest_cv ON c.id = latest_cv.circuit_id
    JOIN circuit_version cv ON c.id = cv.circuit_id AND latest_cv.latest_created_at = cv.created_at
	# ADD JOIN HERE IF NEEDED 
ORDER BY c.code;
```
## Lister les noms des services qu'on peut autowire   
```
sfc debug:autowiring --all
```
   
## Debug un service   
```
sfc debug:container # => tous les services
sfc debug:container NomDuService --show-arguments
```
