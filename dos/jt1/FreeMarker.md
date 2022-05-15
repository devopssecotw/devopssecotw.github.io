# DOS
## JAVA TOOL
### FreeMarker
#### bp
##### bp1
* Use auto escaping
- <#ftl output_format="XML" auto_esc=true>
- <#escape x as x?html>
* Handle missing values
- ?? <#if mouse??> | ?has_content| ! set a default value
* Do not cut off Html
* Consider splitting the template into sub-components.
```markdown
<@s.Results>
...
<#switch s.result.collection>
  <#case "youtube">
    <#include "result_youtube.ftl">
  <#break>
  <#case "web">
    <#include "result_web.ftl">
  <#break>
  <#default>
    <#include "result_default.ftl">
  <#break>
</#switch>
...
</@s.Results>
```
* 

#### references
- <https://freemarker.apache.org/docs/>
- 
