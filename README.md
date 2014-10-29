# EARLY ACCESS

Please be aware there may be bugs, gremlins, and horrible issues; and you could be eaten by a grue. We are not responsible for any loss of life or limb (especially if you are eaten by a grue).

# TeamsnapRb

TeamsnapRb is a convenient wrapper around the faraday and the conglomerate gem that helps you talk to TeamSnap's APIv3.

## Installation

Add this line to your application's Gemfile:

    gem 'teamsnap_rb'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install teamsnap_rb

## Usage


### Config/auth

    # Current app based
    config = TeamsnapRb::Config.new(
      client_id: your_client_id,
      client_secret: your_client_secret
    )
    config.response_middleware << :logger
    client = TeamsnapRb::Client.new(ENV['TEAMSNAP_URL'], config: config)

    # user token based
    config = TeamsnapRb::Config.new(access_token: "your_token")
    config.response_middleware << :logger
    client = TeamsnapRb::Client.new(ENV['TEAMSNAP_URL'], config: config)

### Retrieving

    # me
    # https://apiv3.teamsnap.com/me
    me = client.me.first

    # user id (item property access)
    me.id

    # user's teams
    # https://apiv3.teamsnap.com/teams/search?user_id=USER_ID
    teams = me.teams
    teams = client.teams.search(user_id: me.id)

    # team lookup
    # https://apiv3.teamsnap.com/teams/search?id=777788
    team = client.teams.search(id: 777788).first

    # team members
    # https://apiv3.teamsnap.com/members/search?team_id=777788
    team.members

    # team contacts
    # https://apiv3.teamsnap.com/contacts/search?team_id=777788
    team.contacts

    # team emails
    # https://apiv3.teamsnap.com/contact_email_addresses/search?team_id=777788
    team.contact_email_addresses

    # team phone numbers
    # https://apiv3.teamsnap.com/contact_phone_numbers/search?team_id=777788
    team.contact_phone_numbers

    # team managers
    # https://apiv3.teamsnap.com/members/managers?team_id=777788
    team.managers

    # team events
    # https://apiv3.teamsnap.com/events/search?team_id=777788
    team.events

    # team locations
    # https://apiv3.teamsnap.com/locations/search?team_id=777788
    team.locations

    # team opponents
    # https://apiv3.teamsnap.com/opponents/search?team_id=777788
    team.opponents


### Creating

    # create a user
    Not supported

    # create a team
    create_team_response = client.teams.template.push(
      name: "my new team",
      sport_id: 1,
      location_country: "US",
      time_zone: "Eastern Time (US & Canada)"
    )

    # create a member
    create_member_response = client.members.template.push(
        team_id: TEAM_ID,
        first_name: "first_name",
        last_name: "last_name",
        gender: "gender",
        position: "position",
        address_zip: "address_zip",
        birthday: "birthday"
    )

    # create an event


### Updating

    # update a team
    team = team.with(name: "Updated Team Name")
    team.save


## Contributing

1. Fork it ( http://github.com/teamsnap/teamsnap_rb/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
