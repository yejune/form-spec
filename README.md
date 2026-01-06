# Form-Spec

YAML 기반 폼 생성 및 검증 시스템 (Multi-language, Multi-framework)

## Features

- 🎯 **선언적 폼 정의** - YAML 스펙으로 폼 구조와 검증 규칙 정의
- 🌍 **다중 언어 검증기** - JavaScript/TypeScript, PHP, Go 지원
- ⚛️ **다중 프레임워크** - React (활성), Vue/Svelte (준비 중)
- 📝 **33+ 필드 타입** - 텍스트, 이메일, 날짜, 파일, 주소 검색 등
- ✅ **27개 검증 규칙** - required, email, min/max, pattern 등
- 🔄 **조건부 표시** - 필드 값에 따른 동적 폼 구성
- 🌐 **다국어 지원** - 라벨, 메시지 다국어 처리

## Quick Start

### JavaScript/TypeScript

```bash
npm install @form-spec/validator @form-spec/generator-react
```

```typescript
import { Validator } from '@form-spec/validator';
import { FormBuilder } from '@form-spec/generator-react';

// YAML 스펙 정의
const spec = {
  type: 'group',
  properties: {
    email: {
      type: 'email',
      label: 'Email',
      rules: { required: true, email: true },
      messages: { required: '이메일을 입력하세요' }
    },
    name: {
      type: 'text',
      label: 'Name',
      rules: { required: true, minlength: 2 }
    }
  }
};

// React에서 사용
function App() {
  return (
    <FormBuilder
      spec={spec}
      onSubmit={(data, errors) => console.log(data, errors)}
    />
  );
}

// 서버에서 검증
const validator = new Validator(spec);
const result = validator.validate(formData);
```

### PHP

```bash
composer require form-spec/validator
```

```php
use FormSpec\Validator\Validator;

$validator = new Validator($spec);
$result = $validator->validate($data);
```

### Go

```go
import "github.com/example/form-generator/validator"

v := validator.New(spec)
result := v.Validate(data)
```

## Packages

| 패키지 | 설명 | 상태 |
|--------|------|------|
| [@form-spec/validator](./packages/validator-js) | JavaScript/TypeScript 검증 라이브러리 | ✅ 활성 |
| [@form-spec/generator-react](./packages/generator-react) | React 폼 빌더 컴포넌트 | ✅ 활성 |
| [form-spec/validator (PHP)](./packages/validator-php) | PHP 검증 라이브러리 | ✅ 활성 |
| [validator-go](./packages/validator-go) | Go 검증 라이브러리 | ✅ 활성 |

## Documentation

- [API Reference](./docs/API.md) - Validator API 상세 문서
- [YAML Spec](./docs/SPEC.md) - 스펙 형식 명세서
- [Validation Rules](./docs/VALIDATION-RULES.md) - 검증 규칙 가이드
- [Condition Parser](./docs/CONDITION-PARSER.md) - 조건식 파서 문서

## Examples

- [Demo App](./examples/demo-app/) - 대화형 데모 애플리케이션
- [Playground](./examples/playground/) - 실시간 YAML 편집기
- [Node.js API](./examples/node-api/) - Express 서버 예제
- [PHP API](./examples/php-api/) - PHP 서버 예제
- [Go API](./examples/go-api/) - Go 서버 예제

## Cross-Language Testing

모든 언어의 검증기가 동일한 스펙에 대해 동일한 결과를 반환하는지 검증합니다:

```bash
cd tests
npm run idempotency:all   # JS/PHP/Go 멱등성 검증
```

## Development

```bash
# validator-js 빌드
cd packages/validator-js && npm run build

# generator-react 빌드
cd packages/generator-react && npm run build

# 테스트 실행
npm test
```

## License

MIT
