#[RIOT-API-JAVA]


## Requirements

Requires the following libraries:
- [Google Gson](https://code.google.com/p/google-gson/)


## Setup

You can either compile the library yourself or you can download the compiled .jar file @ https://drive.google.com/file/d/0BxgiDCyluJNvS1ZQcnh2eTlhdUE/view?usp=sharing.
Then add it as an external library to your project. Easy peasy.


## Usage

This library can be used strictly according to the [Riot API Documentation](https://developer.riotgames.com/api/methods) like so:

```java
import java.util.Map;
import constant.Region;
import dto.Summoner.Summoner;
import main.java.riotapi.RiotApi;
import com.google.gson*;

public class Example {

	public static void main(String[] args) {
		
		RiotApi api = new RiotApi("YOUR-API-KEY-HERE");

		Map<String, Summoner> summoners = api.getSummonersByName(Region.NA, ", ");
		Summoner summoner = summoners.get("");
		long id = summoner.getId();
		System.out.println(id);
	}

}

```


Available accessors allow you to accomplish similar tasks in a different way.
Below is an example of how to set your region. Because the region was set before a method was called, there is no need to pass in the region parameter. This is great for people that know they will only be working in one region when making multiple requests. The same can be done for the season.


```java
import java.util.Map;
import constant.Region;
import dto.Summoner.Summoner;
import main.java.riotapi.RiotApi;
import com.google.gson*;

public class Example {

	public static void main(String[] args) {
		
		RiotApi api = new RiotApi("YOUR-API-KEY-HERE");
		
		api.setRegion(Region.NA);
		Map<String, Summoner> summoners = api.getSummonersByName(", ");
		Summoner summoner = summoners.get("");
		long id = summoner.getId();
		System.out.println(id);
	}

}

```


It is important to be aware of your personal rate limit. Any method call from the RiotAPI is a request that counts towards your rate limit, with exceptions to the accessors/mutators of region, key, and season, as well as any requests regarding static data. The below code makes 2 requests; one request for a summoner, and another for ranked stats of a summoner.



```java
import constant.Region;
import constant.Season;
import dto.Stats.RankedStats;
import main.java.riotapi.RiotApi;
import com.google.gson*;

public class Example {

	public static void main(String[] args) {
		
		RiotApi api = new RiotApi("YOUR-API-KEY-HERE", Region.NA);
		api.setSeason(Season.FIVE);
		
		RankedStats rankedStats = api.getRankedStats(api.getSummonersByName(", ").get("").getId());
	}

}

```
