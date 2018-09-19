# This project is the header part of the website

This project was bootstrapped with [Create React App](https://github.com/facebookincubator/create-react-app).

### * Layout: styled-components,Reset.css
Benifit: Every component can be styled separately and Reset.css ensures same default style in different browsers.<br/>
Code sample:
```Javascript
import { injectGlobal } from 'styled-components';

injectGlobal `
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
};
`
```
```Javascript
import styled from 'styled-components'
import logoPic from '../../statics/logo.png';

export const HeaderWarpper = styled.div`
  position: relative;
  height: 58px;
  border-bottom: 1px solid #f0f0f0;
`
export const Logo = styled.a.attrs({
  href: '/'
})`
  position: absolute;
  top:0;
  left: 0;
  display: block;
  width: 100px;
  height: 58px;
  background: url(${logoPic});
  background-size: contain;
`;
```


### * Enbed icon in components with iconfont
Benifit: make components looks special<br/>
Code Sample:
```Javascript
			     <SearchWrapper>
			     <CSSTransition
			     in={props.focused}
			     timeout={200}
			     classNames="slide"
			     >
			     <NavSearch
                 className= {props.focused ? 'focused': ''}
                 onFocus={props.handleInputFocus}
                 onBlur={props.handleInputBlur}
			     ></NavSearch>
			     </CSSTransition>
			     <i className= {props.focused ? 'focused iconfont': 'iconfont'}>&#xe602;</i>
			    
			     </SearchWrapper>
```

### * Use React-Redux framwork
Benifit: Sepatates UI and data control, good for management of the state and the layout of UI and makes easy maitanence of code in future.<br/>
Code sample:
```Javascript
const mapStateToProps = (state) => {
   return {
      focused: state.getIn(['header', 'focused'])
   }
}
const mapDispatchToProps = (dispatch) => {
   return{
     handleInputFocus (){
        dispatch(actionCreators.searchFocus());
     },
     handleInputBlur (){
     	dispatch(actionCreators.searchBlur());
     }
   }
}
export default connect(mapStateToProps, mapDispatchToProps)(Header);
```
```Javascript
import reducer from './reducer';
import * as actionCreators from './actionCreators';
import * as constants from './constants';

export { reducer, actionCreators, constants }
```
```Javascript
import * as constants from './constants';
import { fromJS } from 'immutable';

const defaultState = fromJS({
	focused: false
});

export default (state = defaultState, action)=>{
	if(action.type === constants.SEARCH_FOCUS){
		return state.set('focused', true)
	}
	if(action.type === constants.SEARCH_FOCUS){
		return state.set('focused', false)
	}
    return defaultState;
}
```
### * Use Combine Reducer
Benifit: Combine a reducer with different 'small reducers', and every 'small reducers' controls the data of a section.<br/>
Code sample:
```Javascript
import {combineReducers} from 'redux-immutable';
import {reducer as headerReducer } from '../common/header/store';

const reducer = combineReducers({
	header: headerReducer
});

export default reducer;
```

### * write actions in actionCreator.js and constant in constant.js, which makes easy maitanence of code in future.
Code sample
```Javascript
import * as constants from './constants';

export const searchFocus = () => ({
	type: constants.SEARCH_FOCUS
});

export const searchBlur = () => ({
	type: constants.SEARCH_BLUR
});
```

### * use redux-immutable to manage the data of the page to ensure the immutability of the data.
Code sample:
```Javascript
import * as constants from './constants';
import { fromJS } from 'immutable';

const defaultState = fromJS({
	focused: false
});
```
```Javascript
const mapStateToProps = (state) => {
   return {
      focused: state.getIn(['header', 'focused'])
   }
}
```
