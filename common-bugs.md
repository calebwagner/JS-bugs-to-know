**Loss of function context ```this```.**

**Without solution**
```
  onDelete: function () {
    setTimeout(
      function () {
        this.model.destroy();
        this.remove();
      }
    );
  },
```
---
