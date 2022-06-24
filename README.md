# xRP
Repo for Expected Runs Prevented (xRP) models

xRP is a model that estimates an individual pitch's ability to limit (or allow) runs, based off of how that pitch's characteristics (speed, movement, location, etc) have affected outcomes for similar pitches in the past. Using data from 2017-2021, I estimate the likelihood of a given pitch to be each possible outcome, without including results on balls-in-play (ball, HBP, swinging strike, Line Drive @ 105+mph, etc). I use the average wOBA value for each outcome weighted by the likelihood of that outcome, and sum those outcome wOBAs together, then convert it to a run scale where 0 is the average pitch outcome for that season (positive values "prevent" runs, while negative values "allow" runs). Having this information allows me to estimate various qualities of a pitcher's overall arsenal:

-  I measure how well they locate their pitchers with a Location model that only includes where a pitcher locates the ball at the plate (excludes velocity/movement).

  -I measure how beneficial the physical characteristics of their pitches are with a Stuff model that uses only the pitch's movement & velocity, including how those     characteristics for their off-speed pitches differ from their fastball (excludes location). This model **_only_** looks at the outcomes for swings, as modeling the swing/take decision without location information did not seem intuitively correct.

  -I estimate a pitcher's ability to allow/limit ground balls (launch angle <10 degrees) and their ability to earn Called Strikes + Whiffs (CSW), based off of the average of those expected outcomes across every pitch thrown.

  -I estimate a pitcher's K% & BB% by measuring the likelihood of a Called/Swinging strike in 2-strike counts or a ball in 3-ball counts, respectively.

  -I estimate the likelihood of a pitcher's pitches to result in a home run. This is modelled as its own outcome, and is not included in the Pitching/Location/Stuff model results.

  -I also split these various metrics out by each of the pitch types a pitcher throws (4-Seam Fastball, Slider, Changeup, etc).

xRP is used to determine the effectiveness of a pitcher's individual pitches, but can also be extended to provide context for a batter's decisions and outcomes, and to estimate the value a batter brings in their plate appearances (Expected Runs Added; xRA). Using the quality of the pitches that a batter sees, I estimate various qualities of their approach at the plate:

  -I estimate a batter's judgement of what is a ball or strike by using the likelihoods of a pitch being a called strike, a ball, or a hit-by-pitch (HBP). I assume batters "want" to swing at strikes and take balls/HBPs. I compare when they swing to the likelihood of the pitch being a called strike, and when they take to the likelihood of the pitch being a called ball/HBP. Around the edges of the strikezone, these values will approach a 50/50 split, while pitches that are disctinctly in/out of the strike zone will have a very binary result (Correct/Incorrect).

  -I estimate the value of whether they decide to swing or take. I judge this based on the opportunity cost of their decision, which I calculate as the difference in expected outcome value between a swing and a take, based on the pitch. If they swing, it's (swing value - take value). If they take, its (take value - swing value). Generally, decisions on pitches outside the zone have a stark split in value (takes=good, swings=bad), while inside the zone has more nuance (taking challenging in-zone pitches is rewarded, while swinging at meatballs is also rewarded).

  -I estimate their Contact ability (how often they make contact on a swing compared to the estimated probability of contact) and their Power (the increase in xwOBA they provide based on the ball's launch angle).

  -I also split these estimates out by the pitch types (Fastballs, Breaking Balls, Offspeed Pitches) and strike zone locations the pitches are in.

I put together card-style visualizations for individual pitchers (illustrating how a given pitcher's arsenal works, where they locate their pitches, how those pitches get there, and how valuable those pitches are) and batters (illustrating how they help or hurt themself at the plate, and how they perform against various pitch types and pitch locations). I've been tweeting these out daily at https://twitter.com/blandalytics. I try to post a notable starter/reliever and batter the day after their start/appearance.
