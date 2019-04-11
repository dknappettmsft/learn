# Adding Quotas for the SQL Resource Provider

After you have installed the resource provider, you must configure it so that the resource provider knows which SQL Servers it can use and how much capacity they have available for user consumption. You can also create custom quotas for users to be assigned. There are four default quotas available post-installation that the following table describes.

|Quota Name|Maximum number of Always-On databases|Maximum database size (GB)|Maximum number of databases|
|---------|---------|---------|---------|
|default_BasicTierQuota|0|2|10|
|default_StandardTierQuota|0|250|50|
|default_PremiumTierQuota|100|500|100|
|default_AdminQuota|2147483647|Unlimited|Unlimited|

These quotas are added to the plan you define in Azure Stack, which is in turn is attached to the offer to which users subscribe.