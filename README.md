# R-Code

# An welchem Tag wurde am häufigsten retweetet?

full_tweets$day <- as.Date(format(full_tweets$retweet_created_at,"%D"),format = "%m/%d/%y")

RetweetsPerDay <- aggregate(full_tweets$retweet_status_id ~ full_tweets$day, FUN="length")

names(RetweetsPerDay) = c("day","retweets")


library(ggplot2)
RetweetsPerDay %>%
filter(day >= 2020- 11- 01) %>% ggplot(RetweetsPerDay, aes(x = day, y = retweets)) +
  geom_point(color="green") +
  geom_line(aes(group = 1)) +
  geom_smooth() + xlab("Datum") + ylab("Anzahl der Retweets")


# Der folgende Code funktioniert, eventuell hilft es als Orientierung

## Zu welcher Uhrzeit twittern die Querdenken Nutzer?

full_tweets$hour <- as.numeric(format(full_tweets$created_at,"%H"))

TweetsPerHour <- aggregate(full_tweets$user_id ~ full_tweets$hour, FUN="length")

names(TweetsPerHour) = c("Hour","tweets")

library(ggplot2)
ggplot(TweetsPerHour, aes(x = Hour, y = tweets)) +
  geom_point(color="red") +
  geom_line(aes(group = 1)) +
  geom_smooth() + xlab("Time") + ylab("Number of Tweets")
