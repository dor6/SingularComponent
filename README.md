# SingularComponent
move your react component around the dom

animates your components movement around the dom
just give your wrap ypur component with the SingularComponent and give it a singularKey and a singularPriority

## Install

    npm install react-singular-component

## Usage

here is a component (using semantic ui react) from the example project: 

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

## How does it work

i will render the SingularSearch component twice once with a singularPriority of 1 and once with a singularPriority of 2.
while i render both we will only see the instance with a priority of 2, but i will unmount the higher priority instance the component will move and change to the position and size of the lower priority instance.

here is a gif of the example with the component above:
![alt text](https://image.ibb.co/jJ5Non/example.gif)

please note this is only the start of the this project there is a lot to add.
this is a concept i want to push forward and needs work.
you can download and open the example rar wich contains an example project with the component.

the first thing that needs to be done is to turn this component into a proper npm package (i never did it before so help whould be nice)


# Contribute

simply fork and clone

    cd example
    npm install
    npm start

and you're read to go and make whatever changes you have in mind