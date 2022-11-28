# Pokégotchi : SEI Project 4 - Redeployment     

## Background:      

See original repository and README for this Project [here](https://github.com/hphilpotts/Pokegotchi-Frontend-Project-4-General-Assembly-SEI-66).              

An earlier version was hosted on _Heroku_, however with the closure of their free tier on 28/11/22 I rehosted both frontend and backend elsewhere. In order to make redeployemnt easier, I cloned a 'pre-Heroku' commit from Ashish's original GitHub Enterprise and was able to successfully host this React frontend [on Vercel](https://vercel.com/hphilpotts/pokegotchi-frontend-project-4-general-assembly-sei-66-rehost/BjyUi5YnEWNcredrEx4DLSsFNZyS) - I found the ability to link directly to GitHub super easy, and found navigating settings / environment variables etc. quite straightforward.      

The backend ([repository here](https://github.com/hphilpotts/Pokegotchi-Backend-Project-4-General-Assembly-SEI-66)) is hosted [on Cyclic](https://app.cyclic.sh/#/app/hphilpotts-pokegotchi-backend-project-4-general-assembly-sei-66/overview).        

## Rehosting challenges:        

24/11/22 - 28/11/22     

Whilst hosting the app on Vercel was easy, I found connecting frontend and backend quite problematic for a number of reasons, particularly:     

- Not knowing that `proxy:` in `package.json` only works in _development_, not in _production_. I can comfortably say that I am well aware of this now after a long time wondering why only full urls in `Axios` calls worked...      
- Even once this was resolved, CORS errors we consistently coming up - getting my head around the best way of resolving this took a while, there are a lot of articles and threads out there with a lot of different approaches and ideas on the matter. A positive is that I have a much better understanding of **why** we get CORS errors as well as how to resolve them!             
- Last - _but certainly not least_ - it turns out that `Axios.put` requests that fail validation throw a CORS error. Where Pokégotchi Status values had dropped below negative (they shouldn't do that, see 'Future Improvements' below), requests to update these were failing validation, resulting in a CORS error coming up on the frontend console. This was mighty confusing until I worked out what was going on - I'd got everything working except for the PUT requests in `Card.js` and was trying everything under the sun to bypass the CORS errors!                    

_Key in all of this was_ **Postman** _which might just be my favourite app right now! Without it I would have really, really struggled!_          

## Future Improvements:         

Now that I've got both frontend and backend apps rehosted (_greeaat timing hosting eveything on Heroku a month before they binned their free service_), and indeed talking to each other, there are few changes I'm looking to implement across both apps:       

- _Restrict backend API use only the frontend app only_. At present, the API is publicly accessible - this was to help eliminate certain CORS issues when trying to get the apps to link up.        
- _Implement 'Select a Pokégotchi' upon signup_. We ran out of time to implement this: any new user will not be able to choose a Pokégotchi at present!     
- _Prevent Pokégotchi Status values from decrementing below 0_. I wrongly assumed that the Pokégotchi Model validation parameters would prevent the `Decrement All Pokégotchi Levels API` from lowering these Status values below 0. Instead, values continued (and indeed continue) to go into negatives, and any attempt to change these in the frontend fail (see Rehosting Challenges above). This will require work in the backend only to fix!        

