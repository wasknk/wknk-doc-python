# Type-hints


## SimpleUsage
```python 
from typing import List, TypedDict, Callable

```


## Similarities

it is like TypeScript interface here:
```TypeScript
interface CommentSectionProps {
  comments: Comment[];
  onAddComment: (comment: string) => void;
}

export function CommentSection({ comments, onAddComment }: CommentSectionProps) {
  // ...
}
```