---
layout: post
title:      "More React and CSS Practice"
date:       2019-07-22 15:15:35 -0400
permalink:  more_react_and_css_practice
---


As I continue to learn other languages and frameworks, it is easy to get a bit overconfident in things you have previously learned. I tend to remember all of my projects at a high level, but the low level details can sometimes get a little fuzzy if I haven't recently written similar code. That's why I always try to revisit my past languages and create a simple project. 

My idea was just a simple calendar app. I figured that would give me practice in both CSS and connecting a simple API to store day-to-day tasks. First, I tried established the skeleton of the components. I set up a container component and a stateless calender component. The container determines which month it is and tells the stateless component what to render.

Once I had that, I set to actually create the calendar. I wanted to make a 5 column, 6-7 row block that would contain all my cells. My two components are as follows:

```
const monthLengthHash = {
    January: 31, February: 28, March: 31, April: 30, May:31, June: 30, July: 31, August: 31, September: 30, October: 31, November: 30, December: 31
}

class CalendarContainer extends Component {

    state = {
        month: 'January',
        num_days: 31,
        days: []
    }

    onChange = event => {
        event.preventDefault()
        this.setState({
            month: event.target.value,
            num_days: monthLengthHash[event.target.value]
        })
    }

    onSubmit = event => {
        event.preventDefault()
        this.setState({
            month: event.value
        })
    }

    render(){
        return (
            <>
                <CalendarComponent days={this.state.days} num_days={this.state.num_days}/>
                <br/>
                <form onSubmit={this.onSubmit} id='monthDropdown'>
                    <select value={this.state.month} onChange={this.onChange}>
                        <option value="January">January</option>
                        <option value="February">February</option>
                        <option value="March"> March</option>
                        <option value="April">April</option>
                        <option value="May">May</option>
                        <option value="June">June</option>
                        <option value="July">July</option>
                        <option value="August">August</option>
                        <option value="September">September</option>
                        <option value="October">October</option>
                        <option value="November">November</option>
                        <option value="December">December</option>
                    </select>
                </form>
            </>
        )
    }
}
```
and 
```
const CalendarComponent = props => {

    const calendarArr = []

    for (let i=1; i<=props.num_days; i++){
        calendarArr.push( 
            <div className='cell' key={'day'+i}>       
                <h5 className='cellDay'>{i}</h5>
                <li className='events'>
                    To-do
                </li>
            </div>
        )
    }

    return (
        <div className='calendarComponent'>
            {calendarArr}
        </div>
    )
}
```
I included a drop down menu to select which month is to be displayed. This checks with my constant month-day object to determine number of days and then changes the state. The state.num_days is passed as a prop to the stateless component where it is rendered. My CSS file is:
```
.appContainer {
  width: 800px; 
  margin-left: auto;
  margin-right: auto;
}

.calendarComponent {
  width: 800px
}

.cell {
  border-style: solid;
  width: 150px;
  height: 100px;
  float: left;
}

#monthDropdown {
  clear: left;
  text-align: center;
}
```
I have a container that is 800 pixels wide. Each cell is 150px wide and they float left so there are 5 in a row. My next step is to set up the API and add a fetch request in the componentDidMount method. This will return the tasks that I input into a certain day. 
