# Conceitos SOLID em TypeScript

Os princípios SOLID são um conjunto de diretrizes para a escrita de código orientado a objetos que é fácil de entender, manter e estender. Esses princípios foram definidos por Robert C. Martin e são amplamente adotados na indústria de software. Este guia explica os conceitos SOLID e como aplicá-los em TypeScript.

## Estrutura do Projeto

- /solid-typescript
- |-- /src
- | |-- /examples
- | | |-- single-responsibility.ts
- | | |-- open-closed.ts
- | | |-- liskov-substitution.ts
- | | |-- interface-segregation.ts
- | | |-- dependency-inversion.ts
- |-- .gitignore
- |-- package.json
- |-- README.md
- |-- tsconfig.json

# Princípios SOLID

# S - Princípio da Responsabilidade Única (Single Responsibility Principle - SRP)
## Cada classe deve ter uma única responsabilidade e, portanto, uma única razão para mudar. Em outras palavras, uma classe deve ter apenas um trabalho.

#### Exemplo em TypeScript

```typescript
// Antes
class UserService {
  constructor(private readonly userRepo: UserRepository) {}

  createUser(user: User): void {
    // lógica para criar um usuário
  }

  sendWelcomeEmail(user: User): void {
    // lógica para enviar um email de boas-vindas
  }
}

// Depois
class UserService {
  constructor(private readonly userRepo: UserRepository) {}

  createUser(user: User): void {
    // lógica para criar um usuário
  }
}

class EmailService {
  sendWelcomeEmail(user: User): void {
    // lógica para enviar um email de boas-vindas
  }
}
```

# O - Princípio do Aberto/Fechado (Open/Closed Principle - OCP)
## Classes devem estar abertas para extensão, mas fechadas para modificação. Isso significa que o comportamento de uma classe deve ser extendível sem modificar seu código fonte.
```typescript

Exemplo em TypeScript

// Antes
class Discount {
  getDiscount(type: string): number {
    if (type === 'none') return 0;
    if (type === 'seasonal') return 0.1;
    if (type === 'clearance') return 0.5;
    return 0;
  }
}

// Depois
abstract class Discount {
  abstract getDiscount(): number;
}

class NoDiscount extends Discount {
  getDiscount(): number {
    return 0;
  }
}

class SeasonalDiscount extends Discount {
  getDiscount(): number {
    return 0.1;
  }
}

class ClearanceDiscount extends Discount {
  getDiscount(): number {
    return 0.5;
  }
}
```

# L - Princípio da Substituição de Liskov (Liskov Substitution Principle - LSP)
## Objetos de uma superclasse devem poder ser substituídos por objetos de suas subclasses sem afetar a funcionalidade do programa.
```typescript

Exemplo em TypeScript

// Antes
class Bird {
  fly(): void {
    console.log('Flying');
  }
}

class Penguin extends Bird {
  fly(): void {
    throw new Error('Cannot fly');
  }
}

// Depois
class Bird {
  // Comportamento comum das aves
}

class FlyingBird extends Bird {
  fly(): void {
    console.log('Flying');
  }
}

class Penguin extends Bird {
  // Comportamento específico do pinguim
}
```

# I - Princípio da Segregação de Interfaces (Interface Segregation Principle - ISP)
## Uma classe não deve ser forçada a implementar interfaces que não utiliza. Em vez disso, crie interfaces menores e mais específicas.
```typescript

Exemplo em TypeScript

// Antes
interface Animal {
  eat(): void;
  fly(): void;
  swim(): void;
}

// Depois
interface Eater {
  eat(): void;
}

interface Flyer {
  fly(): void;
}

interface Swimmer {
  swim(): void;
}

class Dog implements Eater {
  eat(): void {
    console.log('Eating');
  }
}

class Eagle implements Eater, Flyer {
  eat(): void {
    console.log('Eating');
  }
  
  fly(): void {
    console.log('Flying');
  }
}

class Fish implements Eater, Swimmer {
  eat(): void {
    console.log('Eating');
  }

  swim(): void {
    console.log('Swimming');
  }
}
```

D - Princípio da Inversão de Dependência (Dependency Inversion Principle - DIP)
Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações. Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.
```typescript

Exemplo em TypeScript

// Antes
class UserService {
  private readonly userRepo = new UserRepository();

  // Métodos da UserService
}

// Depois
interface UserRepo {
  // Métodos da UserRepo
}

class UserRepository implements UserRepo {
  // Implementação dos métodos da UserRepo
}

class UserService {
  constructor(private readonly userRepo: UserRepo) {}

  // Métodos da UserService
}
```

# Conclusão
## Os princípios SOLID são fundamentais para escrever código limpo, modular e escalável. Ao aplicar esses princípios em seus projetos TypeScript, você pode melhorar a manutenibilidade e a extensibilidade do seu código. Compreender e implementar SOLID não só aumenta a qualidade do código, mas também torna o desenvolvimento de software mais eficiente e menos propenso a erros.

## Referências
- Wikipedia: SOLID
- Typescriptlang: Official Website
- Clean Code: A Handbook of Agile Software Craftsmanship by Robert C. Martin
  
## Licença
Este projeto está licenciado sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

# Este `README.md` fornece uma introdução aos princípios SOLID e exemplos de como aplicá-los usando TypeScript.
