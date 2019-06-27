<template>
  <section>
    <div class="columns">
      <div class="column is-half is-offset-one-quarter">
        <h1 class="content"><b>Select your favorite:</b> </h1>
        <b-field label="Find a pokemon">
          <b-autocomplete>

            <template slot-scope="props">
              <div class="media">
                <div class="media-left">
                  <img width="32">
                </div>
                <div class="media-content">
                  {{ props.option.title }}
                  <br>
                  <small>
                    Released at {{ props.option.release_date }},
                    rated <b>{{ props.option.vote_average }}</b>
                  </small>
                </div>
              </div>
            </template>
          </b-autocomplete>
        </b-field>
      </div>
    </div>
  </section>
</template>

<script>
import debounce from "lodash/debounce";

export default {
  data() {
    return {};
  }
};
</script>