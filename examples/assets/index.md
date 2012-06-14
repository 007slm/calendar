# Calendar

## Example

Attached to a field with default options.

<div class="cell">
<input id="date-1" type="text" />
</div>

```javascript
var cal1 = new Calendar({trigger: '#date-1'});
```


Attached to a field with i18n support.

<div class="cell">
<input id="date-2" type="text" />
</div>

```javascript
seajs.use([''../src/calendar', '../src/i18n/zh_CN'], function(Calendar, lang) {
    var cal2 = new Calendar({trigger: '#date-2', lang: lang});
});
```

Attached to a field with Tuesday unavailable.

<div class="cell">
<input id="date-3" type="text" />
<span id="date-3-explain"></span>
</div>

```javascript
var range = function(time) {
    var day = time.day();
    return day != 2;
};
var cal3 = new Calendar({trigger: '#date-3', range: range});
cal3.on('select-disabled-date', function(date) {
    $('#date-3-explain').text('you select a disabled date');
});
```


Related calendars, set range dynamicly.

<div class="cell">
<input id="date-4" type="text" />
<span id="date-4-explain"></span>
<input id="date-5" type="text" />
<span id="date-5-explain"></span>
</div>

```javascript
var cal4 = new Calendar({trigger: '#date-4'});
var cal5 = new Calendar({trigger: '#date-5'});
cal4.on('select-date', function(date) {
    cal5.range([date, null]);
}).on('select-disabled-date', function(date) {
    $('#date-4-explain').text('not available');
});
cal5.on('select-date', function(date) {
    cal4.range([null, date]);
}).on('select-disabled-date', function(date) {
    $('#date-5-explain').text('not available');
});;
```