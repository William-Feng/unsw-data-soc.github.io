---
layout: landing-banner
title: Our Team
permalink: /about/team/
subtitle: Meet the DataSoc team working to create new opportunities for students to connect, grow and feel supported.
---

<link  rel="stylesheet" href="https://unpkg.com/bulma-modal-fx/dist/css/modal-fx.min.css" />
<div class="hero-body background-shade">
    {% assign portfolios = "2022 Team, 2021 Team" | split: ", " %}
    <div class="tabs is-boxed is-centered main-menu is-large" id="nav">
        <ul>
            {% for i in (0..1) %}
            {% if forloop.first == true %}
                {% assign active_status = "is-active" %}
            {% else %}
                {% assign active_status = "" %}
            {% endif %}
            <li data-target="pane-{{ i | plus: 1 }}" id="{{ i | plus: 1 }}" class="{{ active_status }}">
                <a><h2 class="title is-4">{{ portfolios[i] }}</h2></a>
            </li>
            {% endfor %}
        </ul>
    </div>
    <div class="tab-content" style="background:#f0f2f5">
    {% for i in (0..1) %}
        {% assign portfolio = site.team | where:"portfolio", portfolios[i] | sort: "order" %}
        {% if forloop.first == true %}
            {% assign active_status = "is-active" %}
        {% else %}
            {% assign active_status = "" %}
        {% endif %}
        <div class="tab-pane {{ active_status }}" id="pane-{{ i | plus: 1}}" style="background:#f0f2f5">
            <div class="content">
                {% assign remaining_people = portfolio.size %}
                {% for person in portfolio %}
                    <!-- 5 cards per row for 2022 Team (since there are 25 altogether) -->
                    {% if portfolios[i] == "2022 Team" %}
                        {% assign value = forloop.index0 | modulo: 5 %}
                    {% else %}
                        {% assign value = forloop.index0 | modulo: 4 %}
                    {% endif %}
                    <!-- Ways to layout the remaining people in the last row -->
                    {% if value == 0 %}
                        {% if forloop.index0 != 0 %}
                            </div>
                        {% endif %}
                        <div class="columns">
                        {% if remaining_people == 1 %}
                            <div class="column is-4">
                            </div>
                        {% elsif remaining_people == 2 %}
                            <div class="column is-3">
                            </div>
                        {% elsif remaining_people == 3 %}
                            <div class="column is-2">
                            </div>
                        {% endif %}
                    {% endif %}
                        <!-- 5 cards per row for 2022 Team (since there are 25 altogether) -->
                        {% if portfolios[i] == "2022 Team" %}
                            <div class="column is-24">
                        {% else %}
                            <div class="column is-3">
                        {% endif %}
                        <!-- Add information for each card -->
                        {% if person.portfolio == "Subcommittee" %}
                            {% include team-card.html image=person.image name=person.name position=person.position degree=person.degree one_line=person.one_line button_text="Who are we?" %}
                        {% else %}
                            {% include team-card.html image=person.image name=person.name position=person.position degree=person.degree one_line=person.one_line button_text="Who am I?" %}
                        {% endif %}
                        </div>
                        {% include team-modal-card.html name=person.name image=person.image position=person.position degree=person.degree content=person.content one_line=person.one_line %}
                    {% assign remaining_people = remaining_people | minus: 1 %}
                {% endfor %}
                </div>
            </div>
        </div>
    {% endfor %}
</div>
<script src="/assets/js/modals.js"></script>
