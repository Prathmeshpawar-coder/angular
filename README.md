# angular
interpolation,signal,effect,signal binding ,event binding,componenet ifelse use in html 

app.ts M
import { Component, computed, effect, signal } from '@angular/core';
import { RouterOutlet } from '@angular/router';
import { Profile } from './profile/profile';
import { Login } from './login/login';

@Component({
  selector: 'app-root',
  standalone: true,        // ⭐ REQUIRED
  imports: [RouterOutlet,Profile,Login],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {

  
   eventhandle(eventName:string)
   {
       console.log(eventName);
   }

    btndis=true;

    toggle()
    {
      this.btndis=!this.btndis;//true asel tr false karta ani false asel tr true karta
    }

    count=signal(0);
    color="black";

     updatecount()
     {
      this.count()<130 && this.count.set(this.count()+10)
     }
    constructor()
    {
     effect (()=>
    {
       if(this.count()>=0 && this.count()<39)
      {
        this.color='green'
      }
      else if(this.count()>40 && this.count()<79)
      {
        this.color='orange'
      } else if(this.count()>=80){
         this.color='red'
      }
    })
    }

     
    normal=0;

    normalupdate()
    {
      if(this.normal==10)
      {
        this.normal=0;
      }else{
        this.normal++;
      }
    }



    height =signal(100);
    weight =signal(20);

    area = computed (()=> this.height()*this.weight());

    comsig()
    {
      this.height.set(this.height()+1)
    }



    islogin=signal(false);

    logins()
    {
     this.islogin.update(value => !value);//true asel tr false karta ani false asel tr true karta
    
    }
}

app.html M


<app-login></app-login>
<app-profile></app-profile>
<!-- <input type="text" (input)="eventhandle($event)">
<p>{{disp}}</p> -->

<input type="text" (input)="eventhandle($event.type)">

<div class="div1" (mouseenter)="eventhandle($event.type)" ></div>

<div class="div2" (mouseleave)="eventhandle($event.type)"   (mouseenter)="eventhandle($event.type)"></div><br>


<!-- property binding  -->
<button disabled >click me</button>
<button [disabled]="btndis" >click me</button>
<input type="checkbox" (change)="toggle()"> terms and condition
<button (click)="toggle()" >toggle</button><br><br>

<!-- signal -->
<button (click)="updatecount()" >speed increass</button>
<p [style.color] ="color" >{{count()}}</p>

<br><br>

<!-- signal -->
<button (click)="normalupdate()" >update normal</button>
{{normal}}


<br><br>


<!-- computed signal   -->
<button (click)="comsig()" >update height</button>
{{area()}}

<div >
    @if (islogin())
    {
        <span style="color: green;">Welcome users</span><br>
        <button class="logbtn" (click)="logins()" >logout</button><br><br>
     }  @else{
        <span style="color: rgb(195, 10, 10);">login kr bhai </span><br>
        <button class="logbtn" (click)="logins()" >log      in</button><br><br>
     } 
</div>

app.css 
p{
   font-size: 33px;
    font-weight: 900;
    font-family: "Courier New", Courier, monospace;
    color: red;
}
.div1{
    height: 100px;
    width:100px;
    background-color:red;
}
.div2{
    height: 100px;
    width:100px;
    background-color:rgb(8, 105, 6);
}


