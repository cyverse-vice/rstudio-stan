# FOR FUTURE NOTICE: IF YOU WANT TO INSTALL PACKAGES HERE
# INSTALL THEM INSTEAD IN RSTUDIO/VERSE
FROM harbor.cyverse.org/vice/rstudio/verse:latest

# copying the .R folder with Makevars
COPY build_imports/.R /home/rstudio/.R

# rstudio owns ~
# RUN chown -R rstudio:rstudio /home/rstudio/

# installing rstan
RUN install2.r --error --deps TRUE \
    rstan \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# installing Rcpp
RUN install2.r --error --deps FALSE \
    Rcpp \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# installing JAGS
RUN install2.r --error --deps FALSE \
    rjags \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# installing Rcpp
RUN install2.r --error --deps FALSE \
    reshape2 \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# need to get graph as a dep for igraph
RUN R -e "BiocManager::install('graph')"

# direct installs of a few more deps
RUN install2.r --error --deps TRUE \
    igraph \
    posterior \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

# cmdstanr as a dep for brms
RUN install2.r --error --deps TRUE -r "https://mc-stan.org/r-packages/" \
    cmdstanr \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

RUN install2.r --error --deps TRUE \
    brms \
    tidybayes \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds
