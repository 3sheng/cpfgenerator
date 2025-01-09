# CPF Generator API Documentation

## Document Introduction

CPF Generator ([cpfgenerator.org](https://cpfgenerator.org)) provides high-performance, reliable Brazilian tax number generation services, including CPF (Individual Taxpayer Number) and CNPJ (Company Taxpayer Number) generation APIs.

### Product Advantages

- **Accuracy**: Strictly follows the validation algorithm of Brazilian Federal Revenue Service
- **Easy Integration**: Provides integration examples for mainstream programming languages
- **Free to Use**: No registration required, direct API access

## API Overview

- **Protocol**: HTTPS
- **Method**: POST
- **Data Format**: JSON
- **Character Encoding**: UTF-8
- **Base URL**: `https://cpfgenerator.org/api`
- **API Version**: v1

## API List

### 1. CPF API

#### 1.1 CPF Generator

##### 1.1.1 Interface Description

Generate valid Brazilian Individual Taxpayer Numbers (CPF).

- **Endpoint**: `/cpf/generator`
- **Method**: POST
- **Content-Type**: application/json

##### 1.1.2 Request Parameters

| Parameter | Type    | Required | Default | Description |
|-----------|---------|----------|----------|-------------|
| quant     | integer | No       | 1        | Number of CPFs to generate (1-100) |
| format    | boolean | No       | true     | Whether to format the numbers |

###### Request Example

```json
{
  "quant": 2,
  "format": true
}
```

##### 1.1.3 Response Parameters

| Parameter | Type    | Required | Description |
|-----------|---------|----------|-------------|
| success   | boolean | Yes      | Whether the request was successful |
| data      | array   | No       | List of generated numbers |
| count     | integer | No       | Number of generated numbers |
| error     | string  | No       | Error type |
| message   | string  | No       | Error message |

###### Success Response Example

```json
{
  "success": true,
  "data": [
    "123.456.789-09",
    "987.654.321-00"
  ],
  "count": 2
}
```

###### Error Response Example

```json
{
  "success": false,
  "error": "Invalid request format",
  "message": "Parameter \"quant\" must be between 1 and 100"
}
```

##### 1.1.4 Example Code

###### CURL

```bash
curl --location --request POST 'https://cpfgenerator.org/api/cpf/generator' --header 'Content-Type: application/json' --data-raw '{
    "quant": 2,
    "format": true
}'
```

#### 1.2 CPF Validator

##### 1.2.1 Interface Description

Validate Brazilian Individual Taxpayer Numbers (CPF).

- **Endpoint**: `/cpf/validator`
- **Method**: POST
- **Content-Type**: application/json

##### 1.2.2 Request Parameters

| Parameter | Type   | Required | Description |
|-----------|--------|----------|-------------|
| values    | string | Yes      | CPF numbers to validate (comma-separated) |
| format    | boolean | No      | Whether to format the response numbers |

###### Request Example

```json
{
  "values": "319.982.747-05,41950456900",
  "format": true
}
```

##### 1.2.3 Response Parameters

| Parameter | Type    | Required | Description |
|-----------|---------|----------|-------------|
| success   | boolean | Yes      | Whether the request was successful |
| data      | object  | No       | Response data object |
| error     | string  | No       | Error type |
| message   | string  | No       | Error message |

###### Success Response Example

```json
{
    "success": true,
    "data": {
        "results": [
            {
                "cpf": "319.982.747-05",
                "isValid": true
            },
            {
                "cpf": "419.504.569-00",
                "isValid": true
            }
        ],
        "summary": {
            "total": 2,
            "valid": 2,
            "invalid": 0
        }
    }
}
```

###### Error Response Example

```json
{
  "success": false,
  "error": "Invalid request format",
  "message": "Parameter \"quant\" must be between 1 and 100"
}
```

##### 1.2.4 Example Code

###### CURL

```bash
curl --location --request POST 'https://cpfgenerator.org/api/cpf/validator' --header 'Content-Type: application/json' --data-raw '{
  "values": "319.982.747-05,41950456900",
  "format": true
}'
```

### 2. CNPJ API

#### 2.1 CNPJ Generator

##### 2.1.1 Interface Description

Generate valid Brazilian Company Taxpayer Numbers (CNPJ).

- **Endpoint**: `/cnpj/generator`
- **Method**: POST
- **Content-Type**: application/json

##### 2.1.2 Request Parameters

| Parameter | Type    | Required | Default | Description |
|-----------|---------|----------|----------|-------------|
| quant     | integer | No       | 1        | Number of CNPJs to generate (1-100) |
| format    | boolean | No       | true     | Whether to format the numbers |

###### Request Example

```json
{
  "quant": 2,
  "format": true
}
```

##### 2.1.3 Response Parameters

| Parameter | Type    | Required | Description |
|-----------|---------|----------|-------------|
| success   | boolean | Yes      | Whether the request was successful |
| data      | array   | No       | List of generated numbers |
| count     | integer | No       | Number of generated numbers |
| error     | string  | No       | Error type |
| message   | string  | No       | Error message |

###### Success Response Example

```json
{
    "success": true,
    "data": [
        "19.909.725/2666-64",
        "56.624.829/3453-62"
    ],
    "count": 2
}
```

###### Error Response Example

```json
{
    "success": false,
    "error": "Invalid parameters",
    "message": "Parameter \"quant\" must be between 1 and 100"
}
```

##### 2.1.4 Example Code

###### CURL

```bash
curl --location --request POST 'https://cpfgenerator.org/api/cnpj/generator' --header 'Content-Type: application/json' --data-raw '{
    "quant": 2,
    "format": true
}'
```

#### 2.2 CNPJ Validator

##### 2.2.1 Interface Description

Validate Brazilian Company Taxpayer Numbers (CNPJ).

- **Endpoint**: `/cnpj/validator`
- **Method**: POST
- **Content-Type**: application/json

##### 2.2.2 Request Parameters

| Parameter | Type   | Required | Description |
|-----------|--------|----------|-------------|
| values    | string | Yes      | CNPJ numbers to validate (comma-separated) |
| format    | boolean | No      | Whether to format the response numbers |

###### Request Example

```json
{
  "values": "95.811.069/0676-05,68804717558953",
  "format": true
}
```

##### 2.2.3 Response Parameters

| Parameter | Type    | Required | Description |
|-----------|---------|----------|-------------|
| success   | boolean | Yes      | Whether the request was successful |
| data      | object  | No       | Response data object |
| error     | string  | No       | Error type |
| message   | string  | No       | Error message |

###### Success Response Example

```json
{
    "success": true,
    "data": {
        "results": [
            {
                "cnpj": "95.811.069/0676-05",
                "isValid": true
            },
            {
                "cnpj": "68.804.717/5589-53",
                "isValid": true
            }
        ],
        "summary": {
            "total": 2,
            "valid": 2,
            "invalid": 0
        }
    }
}
```

###### Error Response Example

```json
{
    "success": false,
    "error": "Invalid parameters",
    "message": "Parameter \"format\" must be a boolean"
}
```

##### 2.2.4 Example Code

###### CURL

```bash
curl --location --request POST 'https://cpfgenerator.org/api/cnpj/validator' --header 'Content-Type: application/json' --data-raw '{
  "values": "93.387.167/7658-35,48.599.817/3114-00",
  "format": true
}'
```

## Best Practices

1. Use the `quant` parameter for batch generation to avoid multiple requests
2. Set reasonable request timeout values
3. Implement retry mechanism, recommended maximum 3 retries
4. Control concurrent requests reasonably during peak periods

## Support

- Website: [cpfgenerator.org](https://cpfgenerator.org)
- Documentation: [cpfgenerator.org/docs](https://cpfgenerator.org/docs)
- Email Support: contact@cpfgenerator.org
