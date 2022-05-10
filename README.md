# Inline calendar tool for Telebot <PyTelegramBotAPI>
Basic inline calendar for Telegram bots written in Python using [PyTelegramBotAPI](https://github.com/eternnoir/pyTelegramBotAPI). Based on [calendar-telegram](https://github.com/unmonoqueteclea/calendar-telegram).
## Description
The user can either select a date or move to the next or previous month by clicking a singe button.

## Internals
This libruary provides the user with two methods:
* **create_calendar**: This method returns a InlineKeyboardMarkup object with the calendar in the provided year and month.
* **process_calendar_selection:** This method can be used inside a CallbackQueryHandler method to check if the user has selected a date or wants to move to a different month. It also creates a new calendar with the same text if necessary.

## Usage
To use the tele-calendar you need to have [PyTelegramBotAPI](https://github.com/eternnoir/pyTelegramBotAPI) installed first. As you can see below, you create a calendar and add it to a message with a *reply_markup* parameter and then you can process it in a callbackqueyhandler method using the *process_calendar_selection* method:
```python
from tele_calendar import create_calendar, process_calendar_selection
 
  
def calendar_handler(message):
    bot.reply_to(message, "Please select a date: ",
                        reply_markup=create_calendar())
  

@bot.callback_query_handler(func=lambda call: call.data.startswith('DATE'))
def calendar_callback_handler(call):
    is_date_chosen, date = process_calendar_selection(call, bot)
    if is_date_chosen:
        bot.edit_message_text('You have chose %s' % date.strftime('%d:%m:%Y'),
            call.message.chat.id, call.message.id)

```
