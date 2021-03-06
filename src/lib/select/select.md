`<md-select>` is a form control for selecting a value from a set of options, similar to the native
`<select>` element. You can read more about selects in the
[Material Design spec](https://material.google.com/components/menus.html).

<!-- example(select-overview) -->

### Simple select

In your template, create an `md-select` element. For each option you'd like in your select, add an
`md-option` tag. Note that you can disable items by adding the `disabled` boolean attribute or
binding to it.

*my-comp.html*
```html
<md-select placeholder="State">
   <md-option *ngFor="let state of states" [value]="state.code">{{ state.name }}</md-option>
</md-select>
```

### Getting and setting the select value

The select component is set up as a custom value accessor, so you can manipulate the select's value using
any of the form directives from the core `FormsModule` or `ReactiveFormsModule`: `ngModel`, `formControl`, etc.

*my-comp.html*
```html
<md-select placeholder="State" [(ngModel)]="myState">
   <md-option *ngFor="let state of states" [value]="state.code">{{ state.name }}</md-option>
</md-select>
```

*my-comp.ts*
```ts
class MyComp {
  myState = 'AZ';
  states = [{code: 'AL', name: 'Alabama'}...];
}
```

### Resetting the select value

If you want one of your options to reset the select's value, you can omit specifying its value:

*my-comp.html*
```html
<md-select placeholder="State">
   <md-option>None</md-option>
   <md-option *ngFor="let state of states" [value]="state.code">{{ state.name }}</md-option>
</md-select>
```

### Setting a static placeholder

It's possible to turn off the placeholder's floating animation using the `floatPlaceholder` property. It accepts one of three string options:
- `'auto'`: This is the default floating placeholder animation. It will float up when a selection is made.
- `'never'`: This makes the placeholder static. Rather than floating, it will disappear once a selection is made.
- `'always'`: This makes the placeholder permanently float above the input. It will not animate up or down.

```html
<md-select placeholder="State" [(ngModel)]="myState" floatPlaceholder="never">
   <md-option *ngFor="let state of states" [value]="state.code">{{ state.name }}</md-option>
</md-select>
```

Global default placeholder options can be specified by setting the `MD_PLACEHOLDER_GLOBAL_OPTIONS` provider. This setting will apply to all components that support the floating placeholder.

```ts
@NgModule({
  providers: [
    {provide: MD_PLACEHOLDER_GLOBAL_OPTIONS, useValue: { float: 'always' }}
  ]
})
```

### Customizing the trigger label
If you want to display a custom trigger label inside a select, you can use the `md-select-trigger` element:

```html
<md-select placeholder="Favorite food" #select="mdSelect">
  <md-select-trigger>You have selected: {{ select.selected?.viewValue }}</md-select-trigger>
  <md-option *ngFor="let food of foods" [value]="food.value">{{ food.viewValue }}</md-option>
</md-select>
```

Here are the available global options:

| Name            | Type    | Values              | Description                               |
| --------------- | ------- | ------------------- | ----------------------------------------- |
| float           | string  | auto, always, never | The default placeholder float behavior.   |

### Keyboard interaction
- <kbd>DOWN_ARROW</kbd>: Focus next option
- <kbd>UP_ARROW</kbd>: Focus previous option
- <kbd>ENTER</kbd> or <kbd>SPACE</kbd>: Select focused item
