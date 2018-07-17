# SingularComponent
Move your react component around the dom

Transition from one component to another component seamlessly.
Use this for better user exprience, helping them understand its the same component.
Just wrap your components with the SingularComponent, give them the same singularKey, 
and a singularPriority to choose which one of them to show(higher priority will show the componenet).

## Install

    npm install react-singular-component -S

## Usage

Here is a component (using semantic ui react) from the example project: 

```jsx
import SingularComponent from 'react-singular-component';

class SingularSearch extends Component{

    constructor(props){
        super(props);
    }

    handleRef(element){
        element.getElementsByTagName('input')[0].focus();
    }

    render(){
        const {singularPriority, style, value, onChange} = this.props;

        return <SingularComponent singularKey="SingleInput" singularPriority={singularPriority}>
            <Ref innerRef={this.handleRef}>
                <Input icon="search" value={value} style={style} onChange={onChange} />
            </Ref>
        </SingularComponent>;
    }
}
```

I will render the SingularSearch component twice once with a singularPriority of 1 and once with a singularPriority of 2.
while i render both we will only see the instance with a priority of 2, but i will unmount the higher priority instance the component will move and change to the position and size of the lower priority instance.


## Props

<table class="table table-bordered table-striped">
    <thead>
    <tr>
        <th style="width: 100px;">name</th>
        <th style="width: 50px;">type</th>
        <th style="width: 50px;">default</th>
        <th style="width: 50px;">Required</th>
        <th>description</th>
    </tr>
    </thead>
    <tbody>
        <tr>
          <td>singularKey</td>
          <td>String</td>
          <td></td>
          <td>Required</td>
          <td>The library will make sure you always have only one SingularComponent with that key</td>
        </tr>
        <tr>
          <td>singularPriority</td>
          <td>Number</td>
          <td></td>
          <td>Required</td>
          <td>The library will keep only the one with the lower priority for every common singularKey</td>
        </tr>
        <tr>
          <td>children</td>
          <td>React element</td>
          <td></td>
          <td></td>
          <td>The element itself you want to keep single</td>
        </tr>
        <tr>
          <td>animationDuration</td>
          <td>Number</td>
          <td>300</td>
          <td></td>
          <td>Miliseconds duration</td>
        </tr>
        <tr>
          <td>animationTrigger</td>
          <td>Any</td>
          <td>0</td>
          <td></td>
          <td>Any input that when change will trigger an animation of the component, useful for cases when we want to animate the component when a state outside the scope of the component is changed. For example if a sibling component is moved and it will affect the component location, we can give the component as trigger its number of brothers. </td>
        </tr>
        <tr>
          <td>onAnimationBegin</td>
          <td>() => void</td>
          <td></td>
          <td></td>
          <td>callback when the animation begins</td>
        </tr>
        <tr>
          <td>onAnimationComplete</td>
          <td>() => void</td>
          <td></td>
          <td></td>
          <td>Callback when the animation ends</td>
        </tr>
        <tr>
          <td>customTransitionElement</td>
          <td>React element</td>
          <td>The previous element will be taken</td>
          <td></td>
          <td>You can use it to replace the element that transitioned from one element to another</td>
        </tr>
        <tr>
          <td>easing</td>
          <td>(Number) => Number</td>
          <td>EasingFunctions.Linear</td>
          <td></td>
          <td>Given the progress, return the easing progress value. See here: https://easings.net/ . You can import easing functions like that: ```import SingularComponent, {EasingFunctions} from 'react-singular-component'; EasingFunctions.easeOutCubic``` or make your own function</td>
        </tr>
         <tr>
          <td>useStyleAnimation</td>
          <td>Boolean</td>
          <td>false</td>
          <td></td>
          <td>when true animation will use width, height and fontSize to animate dimensions, instead of transform: scale. this can be useful in a lot of cases, for example when height and width ratio changes</td>
        </tr>
         <tr>
          <td>customAnimationHandlers</td>
          <td>['width','height','fontSize', (element, valueFormula, startSnapshot, targetSnapshot) => void]</td>
          <td></td>
          <td></td>
          <td>choose your own animation (which will be added to the position animation), provide your array of changes in addition to existing style animation. provide an array of supported styles you want to animate, in addition to your own custom function to animate yet unimplemented styles or more advance animation.
    customAnimationHandler get as arguments:
              <br/>
              - element: the animated element to change.
              <br/>
              - valueFormula: (startValue(number), endValue(number)) => currentValue(number), use the targetSnapshot and endSnapshot to choose calculate the values of the styles you want to animate 
              <br/>
              - startSnapshot: contains rect(getBoundingClientRect) and style(getComputedStyle) of element before the animation started
              <br/>
              - targetSnapshot: same as startSnapshot but of the element end state of the animation
              <br/>
              <br/>
              ~~~snapshots explained~~~
              <br/>
              startSnapshot belongs to the instance of the component we animating from and target snapshot belongs to the instace of the component we are animating to
            </td>
        </tr>
        <tr>
          <td>extraSnapshotStyleAttributes</td>
          <td>Array of style attributes in camelCase</td>
          <td>[]</td>
          <td></td>
          <td>Add the given style attributes to the style snapshot they will be joined with the customAnimtionHandlers provided by their name ('width', 'fontSize'...). use this when you make your own customAnimationHandler and the given snapshot isnt enough. ( copying all the styles to the snapshot is to heavy )</td>
        </tr>
    </tbody>
</table>
