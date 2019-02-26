<button id= "toggle_{{foo}}" onclick="hiddencode('{{ foo }}')">Hide/Show {{ site.data.xml[foo].file }}</button>
<div id="{{ foo }}" style="display:none">
{% capture text-capture %}
{% raw %}
```
{% include {{ site.data.xml[foo].file }} %}
```
{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>
