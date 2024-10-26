# Create a topic
```bash
gcloud pubsub topics create sandiego
```

# Publish to topic
```bash
gcloud pubsub topics publish sandiego --message "hello"
```

```python
import os
from google.cloud import pubsub_v1

topic_name = 'projects/{project_id}/topics/{topic}'.format(
  project_id=os.getenv('GOOGLE_CLOUD_PROJECTS'),
  topic='MY_TOPIC_NAME',
)

publisher.create_topic(topic_name)
publisher.publish(topic_name, b'My first message!', author='dylan')
```

# Subscribing with Pub/Sub using async pull
```python
import os
from google.cloud import pubsub_v1

subscriber = pubsub_v1.SubscriberClient()
topic_name = 'projects/{project_id}/topics/{topic}'.format(
  project_id=os.getenv('GOOGLE_CLOUD_PROJECT'),
  topic='MY_TOPIC_NAME',
)
subscription_name = 'projects/{project_id}/subscriptions/{sub}'.format(
  project_id=os.getenv('GOOGLE_CLOUD_PROJECT'),
  sub='MY_SUBSCRIPTION_NAME',
)
subscriber.create_subscription(
  name=subscription_name, topic=topic_name
)

def callback(message):
  print(message.data)
  message.ack()

future = subscriber.subscriber(subscription_name, callback)
```
