# GRAPHQL

---

### WhAT is typeDefs and resolvers

---

#### typeDef : 데이터의 타입에 대해서 선언.

```
const typeDefs = gql`
  type Query {
    teams: [Team]
  }
  type Team {
    manager: String
    mascot: String
    cleaning_duty: String
    project: String
  }
`
```

해당 방식으로 typeDefs 를 선언하게 되면 아래와 같이 질의를 던질수 있다.

```
query {
    teams {
        manager
    }
}
```

- 위와 같이 쿼리는 teams 라는 질의를 가질수 있고 그 이외에 타입에 대해서 선언하더라도 query 에 타입을 추가해주지 않았기 때문에 질의를 던질 수 없다.

#### resolver : 실제로 액션이 발생했을때 무엇을 return 해줄수 있는지 지정.

```
const resolvers = {
  Query: {
    teams: () => database.teams,
  },
};
```

- query / teams 로 질의를 했을때, databse.teams 를 return 해주도록 매핑하고있다.
- teams 데이터에 실제로 id, office 등 다른데이터가 있지만 아래와 같이 질의할수 없다.

```
query {
    teams {
        id,
        office
    }
}
```

- 위와 같이 질의하기 위해선 typeDef 에서 타입을 매핑해줘야 한다.
