# TypeScript Codable [![npm](https://img.shields.io/npm/v/ts-codable)](https://www.npmjs.com/package/ts-codable) [![npm bundle size](https://img.shields.io/bundlephobia/minzip/ts-codable)](https://www.npmjs.com/package/ts-codable)

another strict json parser inspired by [Swift Codable](https://developer.apple.com/documentation/swift/codable) ❤️

![Alt text](docs/cover.png 'Title')

## Features

Works almost same as [Swift Codable](https://developer.apple.com/documentation/swift/codable), but with some extra implementation to fit `TypeScript` / `JavaScript` environment.

- Decodes `JSON` payload with pre-defined scheme.
  - Custom keys parsing.
  - Strict types checking.
  - Nested `Codable` parsing.

## Supported Types

Types design was inspired by [MobX State Tree](https://github.com/mobxjs/mobx-state-tree#types-overview) ❤️

- Primitives
  - String
  - Number
  - Boolean
- Complex
  - Codable
  - Optional
  - Array
  - Date

## Installation

```bash
yarn add ts-codable
# or
npm install ts-codable
```

## Usage

```ts
import { BaseCodable, types, decode } from 'ts-codable';
import dayjs from 'dayjs';

class Post extends BaseCodable {
  title!: string;
  isActive?: boolean;
  date!: Date;
}

Post.CodingProperties = {
  title: types.string,
  isActive: {
    type: types.optional(types.boolean),
    key: 'active',
  },
  date: types.date(dayjs),
};

class User extends BaseCodable {
  id!: number;
  username!: string;
  posts!: Post[];
}

User.CodingProperties = {
  id: types.number,
  username: types.string,
  posts: types.array(Post),
};

const jsonPayload = {
  id: 123,
  username: 'Gorhom',
  posts: [
    {
      title: 'dummy post',
      active: true,
      date: '2020-02-15T16:00:00.000Z',
    },
    {
      title: 'deleted post',
      active: false,
      date: '2020-02-10T16:00:00.000Z',
    },
  ],
};

const user: User = decode(User, jsonPayload);
```

## TODO

- [x] Add [Swift Decodable](https://developer.apple.com/documentation/swift/decodable) functionality.
- [ ] Add [Swift Encodable](https://developer.apple.com/documentation/swift/encodable) functionality.
- [ ] Write API docs.

## Built With

- [TSdx](https://github.com/jaredpalmer/tsdx) - Zero-config TypeScript package development.
- [TypeScript](https://github.com/Microsoft/TypeScript) - Strict syntactical superset of JavaScript.

## Author

- [Mo Gorhom](https://twitter.com/gorhom)
