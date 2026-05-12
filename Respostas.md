# Exercício Prático: Modelagem e Consultas em MongoDB

---

# Parte 1: Modelagem de Dados

## 1. Incorporação (Embedding)

### Documento do curso
```json
{
  "_id": 1,
  "nome": "Desenvolvimento Web",
  "categoria": "Tecnologia",
  "modulos": [
    {
      "nome": "HTML e CSS",
      "carga_horaria": 20
    },
    {
      "nome": "JavaScript",
      "carga_horaria": 30
    },
    {
      "nome": "Node.js",
      "carga_horaria": 25
    }
  ]
}
```

### Resposta
A incorporação melhora o desempenho porque os módulos ficam dentro do próprio documento do curso, permitindo buscar todas as informações em uma única consulta ao banco de dados.

---

## 2. Referência (Reference)

### Documento do instrutor
```json
{
  "_id": 101,
  "nome": "Carlos Silva",
  "especialidade": "Backend"
}
```

### Documento do curso
```json
{
  "_id": 201,
  "nome": "API REST com Node.js",
  "instrutor_id": 101
}
```

### Resposta
A referência é melhor quando o mesmo instrutor está relacionado a vários cursos, evitando duplicação de dados e facilitando atualizações futuras.

---

# Parte 2: Consultas e Filtros

## 1. Filtro de Existência
```javascript
db.clientes.find({
  email: { $exists: true }
})
```

---

## 2. Filtro de Comparação
```javascript
db.clientes.find({
  idade: { $gte: 21 }
})
```

---

## 3. Filtro Complexo
```javascript
db.clientes.find({
  cidade: "São Paulo",
  idade: { $lt: 30 }
})
```

---

# Parte 3: Aggregation Framework (Relatórios)

## Pipeline de agregação
```javascript
db.vendas.aggregate([
  {
    $match: {
      status: "concluída"
    }
  },
  {
    $group: {
      _id: "$categoria",
      total_quantidade: {
        $sum: "$quantidade"
      }
    }
  }
])
```

## Explicação
- `$match` → filtra apenas vendas concluídas.
- `$group` → agrupa os documentos pela categoria.
- `$sum` → soma a quantidade vendida de cada categoria.